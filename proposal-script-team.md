# DeskClaw: Presentation Script

## Slide 1: Title & Introduction
**Visual:** Title Slide - "DeskClaw: Full-Lifecycle Conversational Commerce Agent for Local D2C Brands". Names of team members. A clean, professional logo or graphic (e.g., a simple robot icon next to a smartphone).

**Speaker Script:**
"Good morning, everyone. Today, our team is excited to introduce you to DeskClaw. 

DeskClaw is a project born out of a very specific, modern retail problem. We are building a 'Full-Lifecycle Conversational Commerce Agent'. That’s a lot of buzzwords, but what it really means is that we are creating an AI that acts like a senior salesperson and a customer support lead, specifically designed for local Direct-to-Consumer, or D2C, brands.

If you look at how small local businesses operate today, their entire storefront, their marketing, and their community all live on social media—primarily Instagram and WhatsApp. But when it comes to actually making a sale or handling a complex customer issue, there is a massive disconnect. We built DeskClaw to bridge that gap using advanced, privacy-first, local AI."

## Slide 2: The Problem Statement (The Conversational Bottleneck)
**Visual:** A graphic showing a Shopee storefront and an overflowing Shopee Chat/Instagram inbox. Bullet points: Repetitive Queries, Lost Sales, Rigid Chatbots.

**Speaker Script:**
"To understand why DeskClaw is necessary, let's look at the reality for local sellers here in Asia. 

Most D2C brands rely heavily on platforms like Shopee. Shopee is fantastic for transactions, and yes, it has a built-in seller chat. But here is the reality of customer behavior: product discovery can also happens on apps like Instagram, TikTok, LINE, and Whatsapp. Customers don't want to switch apps just to ask a question—they DM the brand right where they saw the ad. 

Furthermore, even when they do use Shopee chat, they expect instant, personalized answers. Instead, they get Shopee's built-in auto-reply, which is just a static, rigid menu that can't handle complex context or negotiate prices. 

As a result, business owners are forced to juggle overflowing inboxes across multiple platforms. Small teams waste hours manually answering the exact same repetitive questions. Because they can't be online 24/7, they lose potential sales from hesitant buyers who need tailored recommendations. 

The core problem is that businesses cannot effectively scale *conversational sales* across the platforms where their customers actually spend time. That is the gap DeskClaw fills."

## Slide 3: Project Objectives
**Visual:** A clean layout highlighting the Main Objective and three core Business Objectives (Support, Sales, Brand Safety).

**Speaker Script:**
"So, what exactly are we trying to achieve? Our main objective with DeskClaw is to build an intelligent, conversational agent that actively drives sales and handles support, while giving businesses full control over their customer data and AI strategy.

We break this down into three core business objectives:

First, we want to **dramatically improve customer support**. The goal is to provide instant, highly accurate answers that are strictly grounded in the business's actual policies, eliminating the frustration of rigid, menu-driven chatbots.

Second, we want to **actively increase sales conversions**. We aim to do this by offering personalized product matchmaking and strategic, margin-aware price negotiations to close hesitant buyers.

Finally, we must **protect the brand's reputation**. We need a fail-safe system that detects when a customer becomes frustrated and immediately escalates the conversation to a human manager before a situation escalates."

## Slide 4: Proposed Methodology
**Visual:** A central "Smart Orchestration Gateway" (OpenClaw) connected to a "Frozen LLM" (`gemma4:e4b`). Three branching paths extend from the gateway, labeled: 1. Support (RAG), 2. Sales (Tool Calling), 3. Safety (Sentiment).

**Speaker Script:**
"To deliver on those three business goals, we cannot rely on a standard, rigid chatbot. But we also don't want the massive expense of retraining a custom AI model from scratch. 

Our proposed methodology will solve this using what we call a **'Smart Orchestration' architecture**. 

If you look at the diagram, the 'brain' of our planned system will be a frozen foundation model—specifically the local `gemma4:e4b` model. But the true power will lie in the 'hands' of the system: our OpenClaw Gateway. Instead of the AI guessing answers, the Gateway will intercept the conversation and give the AI access to specific external tools based on what the user needs.

Here is how the workflow will operate in practice:

**When a customer needs Support**, the system will trigger our *Policy Oracle*. This will use Retrieval-Augmented Generation, or RAG, to search the company's local markdown files and inject the exact policy into the chat.

**When a customer wants to Buy**, the system will switch to Tool Calling. Our *Personalized Matchmaker* will query the product database to find the right item, and our *Dynamic Negotiator* will be able to actually generate unique promo codes to close the deal within approved margins.

**And running constantly in the background will be our Safety Net.** We will deploy a zero-shot sentiment classifier to monitor the emotional tone. If it detects frustration, the orchestration gateway will halt the AI and flag a human manager.

By separating the 'brain' from the 'tools', we will create a highly capable system that is private, affordable, and deeply integrated into the business."

## Slide 5: Technical Execution (How We Build It)
**Visual:** A segmented architectural diagram. The foundational layer shows a "Shipping Container" icon labeled "Docker Dev Container (Standardized & Cloud-Ready)". [More visual elements will be added to this diagram as we discuss them].

**Speaker Script:**
"Moving from what we are building to exactly how we will execute it. 

Our first step is the infrastructure. We will build DeskClaw entirely inside a Docker Dev Container. 

We chose this approach to eliminate the classic 'it works on my machine' problem. By using Docker, we package the AI, its tools, and its environment into one isolated container. This means that when the prototype is finished, we can deploy it directly to any company's cloud server, and it will run exactly as it did in development, without requiring complex setup or troubleshooting.

**Visual Update:** Above the container layer, add an "OpenClaw Gateway" block connecting to two side-by-side modules: "Local AI Engine (gemma4/Ollama)" and a plug-and-play icon showing options for "OpenAI / Claude".

**Speaker Script (Part 2: The Orchestrator & The Engine):**
"Once the foundation is set, we will build the 'engine' and the 'orchestrator' of DeskClaw.

For the AI engine itself, we will run the `gemma4` model locally using a tool called Ollama. We will do this for a very specific business reason: zero inference costs. We can test, refine, and stress-test the AI a thousand times over during prototyping without paying a single cent in API fees. 

But an AI is just a brain; it needs hands to act. That is where our orchestrator comes in. 

Using Node.js, we will deploy the OpenClaw framework as our WebSocket Gateway. Think of this Gateway as the ultimate middleman. It sits between the customer on their phone and the AI, executing the specific 'Skills' we build—like checking live inventory or actually generating promo codes. 

Most importantly, OpenClaw makes our entire architecture model-agnostic. While we will build the prototype using the free, local `gemma4` model, a future business owner could swap it out for OpenAI's ChatGPT in seconds if they needed more reasoning power, without changing a single line of our core code. We are building for maximum flexibility."

**Visual Update:** On the left side of the "OpenClaw Gateway" block, add a branch connected to a "Data Layer" box. Inside the box, show two icons: a Document icon ("Markdown Files: Policies") and a Database icon ("SQLite: Product Catalog").

**Speaker Script (Part 3: The Data Layer):**
"The third piece of our methodology is how we will actually give DeskClaw its knowledge. The traditional approach of constantly retraining an AI model is slow and incredibly expensive. We are completely bypassing that problem.

Instead, we will use simple file formats to create a flexible 'Data Layer'.

For unstructured data, like the company’s shipping, returns, and general policies, we will use basic text files written in Markdown. For structured data, like the live product catalog and inventory, we will use lightweight SQLite databases. 

Why does this matter? Because a small business owner shouldn't need a team of data scientists to update their AI. If they want to change their return policy, they simply open a text file, type the new rule, and hit save. If they add a new product, they just update their spreadsheet. DeskClaw will instantly read the new data and start selling based on it, with zero downtime and zero retraining costs."

**Visual Update:** On the right side of the "OpenClaw Gateway" block, add branches connecting to two familiar logos: "WhatsApp Business API" and "Instagram Messaging API". 

**Speaker Script (Part 4: The Interfaces):**
"The final piece of our technical execution is the interface. How does the customer actually interact with DeskClaw?

We are not building a standalone app that no one will download, and we are not forcing users to navigate to a clunky website chat widget. Instead, we will connect the OpenClaw Gateway directly into the messaging platforms that customers are already using every single day. 

For this prototype, we will simulate integrations with the WhatsApp Business API and the Instagram Messaging API. 

From a technical standpoint, OpenClaw will listen for incoming messages on these channels, route them to our AI engine, and instantly send the AI's responses back. But from a business perspective, the value is much simpler: we are removing all friction. We are allowing the business to provide 24/7, personalized service right inside the customer's favorite messaging app."

## Slide 6: Expected Outcomes (Why It Matters)
**Visual:** Three strong metrics/bullet points with icons: "Functional Prototype", "Zero-Wait Responses", and "Guaranteed Brand Safety".

**Speaker Script:**
"To wrap up, what will we actually deliver at the end of this project?

First, we will deliver a fully functional prototype. This won't just be a theoretical slide deck; we will demonstrate a live system that actively queries policies and negotiates prices using local hardware.

Second, we expect to show a massive, measurable reduction in response time for repetitive customer inquiries. By giving the AI instant access to the company's knowledge base, we will completely eliminate the hours owners currently spend answering the same questions every day.

But perhaps most importantly, we will deliver a robust demonstration of our Frustration Safety Net. We know that handing control over to an AI is scary for a business owner. By proving that our system can instantly recognize negative sentiment and hand the conversation back to a human, we will demonstrate that DeskClaw is not just intelligent—it is safe.

Thank you. We are excited to build the future of local commerce, and we'd be happy to take your questions."