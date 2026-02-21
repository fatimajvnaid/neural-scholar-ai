# Neural Scholar AI | Dynamic RAG CV Assistant

An intelligent, fully dynamic Retrieval-Augmented Generation (RAG) assistant that allows users to upload their CVs on the fly and chat with an AI about their professional background, skills, and areas for improvement.

Unlike traditional static RAG models that rely on pre-loaded documents, this project dynamically ingests, embeds, and isolates user documents per session, ensuring complete privacy and real-time processing.

## Key Features
* **Dynamic File Ingestion:** Users upload their own PDFs/Documents directly through the chat interface. No hardcoded data.
* **Session-Isolated Memory:** Utilizes Pinecone namespaces linked to unique Session IDs. User A will never intersect with User B's vector data.
* **100% Free AI Stack:** Engineered to run entirely on free-tier APIs without hitting rate limits.
* **Context-Aware Conversation:** Maintains conversational history using Window Buffer Memory for seamless, human-like follow-up questions.
* **Cyber-Academic Frontend:** A custom-built, responsive HTML/CSS interface featuring glassmorphism, ambient glows, and a floating n8n chat widget.

## Tech Stack
* **Workflow Automation:** [n8n](https://n8n.io/)
* **Vector Database:** [Pinecone](https://www.pinecone.io/) (Serverless)
* **LLM / Brain:** Meta Llama 3.3 70B Instruct (via [OpenRouter](https://openrouter.ai/))
* **Embeddings:** Cohere (`embed-english-v3.0`)
* **Frontend:** Vanilla HTML/CSS + JavaScript (n8n Chat UI Integration)

## How it Works (The Architecture)
1. **The Traffic Cop (Logic Routing):** When a user interacts, the workflow checks if a binary file is attached.
2. **Ingestion Path:** If a CV is uploaded, it is split into chunks, converted into vectors via Cohere, and stored in a Pinecone namespace unique to that user's session.
3. **Retrieval Path:** When the user asks a question, the AI Agent uses a dedicated Search Tool to query the specific Pinecone namespace, reads the retrieved context, and generates a personalized response.

## Future Improvements
* Add multi-document support (e.g., CV + Cover Letter).
* Implement custom Cohere Reranking for even higher precision.
