# DeskClaw: Full-Lifecycle Conversational Commerce Agent

## 1. Presentation Title
**DeskClaw: Full-Lifecycle Conversational Commerce Agent for Local D2C Brands**
*Members: [Your Name/Team]*

## 2. Introduction / Background
Local Direct-to-Consumer (D2C) brands increasingly rely on social media platforms (WhatsApp, Instagram) for customer engagement. However, traditional e-commerce platforms (like Shopee or Shopify) act as static digital catalogs lacking conversational interfaces. As a result, businesses struggle to scale personalized customer service and consultative sales, which are crucial for maintaining brand loyalty and driving revenue in modern retail.

## 3. Problem Statement
Small and medium-sized D2C businesses waste hours manually answering repetitive pre- and post-sales questions via Direct Messages. Furthermore, they lose potential sales because they cannot provide immediate, 24/7 personalized product recommendations or negotiate dynamically with hesitant buyers. Existing chatbot solutions are often rigid, robotic, and lack the ability to handle complex context, which actively frustrates customers—especially when they are already experiencing an issue.

## 4. Objectives
**Main Objective:** Develop an intelligent, conversational commerce agent that automates customer service and actively drives sales without requiring businesses to surrender privacy to cloud AI providers.

**Specific Objectives:**
*   Develop a hybrid AI architecture that securely queries business databases and documents without altering the core Large Language Model (LLM).
*   Improve customer satisfaction by providing instant, accurate answers to policy inquiries using Retrieval-Augmented Generation (RAG).
*   Increase sales conversions through personalized product matchmaking and dynamic margin-aware price negotiations via Tool Calling.
*   Reduce the risk of PR disasters by implementing a real-time sentiment analysis layer that automatically routes frustrated users to human agents.

## 5. Proposed Methodology
**Approach:** The system uses a "smart orchestration" architecture that wraps around a frozen, local foundation model. Instead of retraining the model, the system leverages external tools, retrieval mechanisms, and strict prompt engineering to guide the AI's behavior.

**Models:** 
*   Local LLM: `gemma4:e4b` (running via Ollama) to ensure data privacy and zero inference costs.
*   Zero-shot classification for sentiment analysis.

**System Workflow:**
1.  **Policy Oracle (RAG):** The system searches local markdown documents (shipping, returns) to provide instant, accurate answers to policy inquiries, injecting relevant text directly into the LLM's context.
2.  **Personalized Matchmaker (Database Query):** For shopping inquiries, the LLM extracts user requirements (e.g., "quiet keyboard") and triggers external functions to query a structured product database, returning personalized recommendations.
3.  **Unboxing Concierge (Deep Linking):** Physical product QR codes contain deep links that initialize a stateful, context-aware chat session, allowing the AI to guide users through complex product setups step-by-step.
4.  **Dynamic Negotiator (Tool Calling):** To close hesitant buyers, the AI dynamically negotiates within pre-defined margin boundaries and triggers a tool to generate unique, one-time e-commerce promo codes.
5.  **Frustration Safety Net (Sentiment Routing):** Operating continuously, a zero-shot sentiment classifier monitors the conversation. If negative emotion is detected, the AI halts and automatically escalates the thread to a human manager.

## 6. Dataset / Data Source
*   **Dataset Name:** DeskClaw D2C Synthetic Knowledge Base
*   **Source:** Custom-generated datasets designed to simulate a realistic local brand.
*   **Type of Data:** 
    *   *Unstructured Data:* Markdown files containing company policies (e.g., shipping, returns, product care).
    *   *Structured Data:* JSON files or lightweight SQLite databases representing a product catalog (including product names, tags, prices, and links) and an inventory state.
*   **Expected Size:** Small-scale (megabytes) optimized for rapid prototyping and testing local RAG pipelines.

## 7. Tools & Technologies
*   **AI Engine:** Ollama running the `gemma4:e4b` local model.
*   **Orchestration / Gateway:** OpenClaw (Node.js/WebSocket hub) to handle tool execution and routing.
*   **Programming Languages:** JavaScript (Node.js) for OpenClaw Skills and Python for data handling (if needed).
*   **Infrastructure:** Docker Dev Container running on Windows WSL2.
*   **Integration Platforms:** WhatsApp Business and Instagram APIs (simulated interfaces for the prototype).

## 8. Expected Outcomes
*   A fully functional prototype demonstrating advanced AI patterns (RAG and Tool Calling) running entirely on local hardware.
*   Measurable reduction in simulated human response time for repetitive policy inquiries.
*   A robust demonstration of an AI agent that seamlessly transitions between automated conversational sales and human intervention based on real-time emotional context (Sentiment Routing).
