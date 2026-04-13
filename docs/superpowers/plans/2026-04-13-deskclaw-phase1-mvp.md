# DeskClaw Phase 1 MVP Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Implement the MVP of DeskClaw, establishing the OpenClaw infrastructure, the "Frustration Safety Net" (Sentiment Routing), and the "Policy Oracle" (RAG) using local markdown files.

**Architecture:** OpenClaw gateway running in a Docker container, interfacing with a local Ollama instance (`gemma4:e4b`). The gateway uses a simple routing script to check incoming messages for negative sentiment (escalating if angry), and falls back to a RAG skill that searches local markdown files to answer customer policy questions.

**Tech Stack:** Node.js (OpenClaw), Ollama (gemma4:e4b), Markdown for knowledge base.

---

### Task 1: Setup OpenClaw Workspace and Configuration

**Files:**
- Create: `deskclaw-workspace/openclaw.config.json`
- Create: `deskclaw-workspace/SOUL.md`
- Create: `deskclaw-workspace/AGENTS.md`

- [ ] **Step 1: Create workspace directories**

```bash
mkdir -p deskclaw-workspace/skills
mkdir -p deskclaw-workspace/knowledge
```

- [ ] **Step 2: Create openclaw configuration**

```json
{
  "gateway": {
    "port": 18789
  },
  "llm": {
    "provider": "ollama",
    "endpoint": "http://host.docker.internal:11434",
    "model": "gemma4:e4b"
  }
}
```
*Save as: `deskclaw-workspace/openclaw.config.json`*

- [ ] **Step 3: Define the core SOUL instructions**

```markdown
You are DeskClaw, a helpful customer service assistant for a local D2C brand.
Your primary goal is to answer customer questions accurately using your knowledge base.
If a customer is angry or frustrated, you must escalate the conversation to a human.
Never invent policies or information not found in your knowledge base.
```
*Save as: `deskclaw-workspace/SOUL.md`*

- [ ] **Step 4: Define the main Agent profile**

```markdown
# main
The default routing agent for DeskClaw.
Skills: `sentiment_router`, `policy_oracle`
```
*Save as: `deskclaw-workspace/AGENTS.md`*

- [ ] **Step 5: Commit workspace setup**

```bash
git add deskclaw-workspace/
git commit -m "chore: setup OpenClaw workspace and configuration"
```

### Task 2: Create Local Knowledge Base

**Files:**
- Create: `deskclaw-workspace/knowledge/shipping.md`
- Create: `deskclaw-workspace/knowledge/returns.md`

- [ ] **Step 1: Write shipping policy**

```markdown
# Shipping Policy
We offer free standard shipping on all orders over $50.
Standard shipping takes 3-5 business days.
Expedited shipping is available for $15 and takes 1-2 business days.
We currently only ship within the contiguous United States.
```
*Save as: `deskclaw-workspace/knowledge/shipping.md`*

- [ ] **Step 2: Write returns policy**

```markdown
# Returns Policy
Items can be returned within 30 days of delivery for a full refund.
Items must be unworn, unwashed, and in their original packaging.
To initiate a return, please email support@example.com with your order number.
Return shipping costs are the responsibility of the customer unless the item was defective.
```
*Save as: `deskclaw-workspace/knowledge/returns.md`*

- [ ] **Step 3: Commit knowledge base**

```bash
git add deskclaw-workspace/knowledge/
git commit -m "docs: add shipping and returns policies to knowledge base"
```

### Task 3: Implement Sentiment Routing Skill (Frustration Safety Net)

**Files:**
- Create: `deskclaw-workspace/skills/sentiment_router.js`

- [ ] **Step 1: Create the sentiment routing skill**

```javascript
export const name = 'sentiment_router';
export const description = 'Analyzes user sentiment and escalates to a human if angry or negative.';
export const parameters = {
  message: { type: 'string', description: 'The user message to analyze' }
};

export async function execute(args, context) {
  const msg = args.message.toLowerCase();
  const negativeWords = ['angry', 'mad', 'furious', 'terrible', 'worst', 'hate', 'refund now', 'smashed', 'broken'];
  
  const isNegative = negativeWords.some(word => msg.includes(word));
  
  if (isNegative) {
    console.log(`[ESCALATION ALERT] Negative sentiment detected in message: "${args.message}"`);
    return "I understand you're frustrated. I've escalated this to our human support team, and they will contact you shortly.";
  }
  
  return "Sentiment is neutral/positive. Proceed with standard response.";
}
```
*Save as: `deskclaw-workspace/skills/sentiment_router.js`*

- [ ] **Step 2: Commit sentiment routing skill**

```bash
git add deskclaw-workspace/skills/sentiment_router.js
git commit -m "feat: implement sentiment routing skill for escalation"
```

### Task 4: Implement Policy Oracle Skill (RAG)

**Files:**
- Create: `deskclaw-workspace/skills/policy_oracle.js`

- [ ] **Step 1: Create the RAG skill**

```javascript
import fs from 'fs';
import path from 'path';

export const name = 'policy_oracle';
export const description = 'Searches the company knowledge base for answers regarding shipping, returns, and policies.';
export const parameters = {
  query: { type: 'string', description: 'The topic to search for (e.g., "shipping", "returns")' }
};

export async function execute(args, context) {
  const query = args.query.toLowerCase();
  let result = "No relevant policy found.";
  
  const kbDir = path.join(process.cwd(), 'deskclaw-workspace', 'knowledge');
  
  try {
    if (query.includes('ship')) {
      result = fs.readFileSync(path.join(kbDir, 'shipping.md'), 'utf-8');
    } else if (query.includes('return') || query.includes('refund')) {
      result = fs.readFileSync(path.join(kbDir, 'returns.md'), 'utf-8');
    } else {
      // Very basic fallback: read all files
      const files = fs.readdirSync(kbDir);
      let combined = '';
      for (const file of files) {
        if (file.endsWith('.md')) {
          combined += fs.readFileSync(path.join(kbDir, file), 'utf-8') + '\n\n';
        }
      }
      result = combined;
    }
  } catch (error) {
    return `Error accessing knowledge base: ${error.message}`;
  }
  
  return `Relevant knowledge base content:\n${result}\nPlease use this to answer the user's question accurately.`;
}
```
*Save as: `deskclaw-workspace/skills/policy_oracle.js`*

- [ ] **Step 2: Commit RAG skill**

```bash
git add deskclaw-workspace/skills/policy_oracle.js
git commit -m "feat: implement policy oracle skill for basic RAG"
```
