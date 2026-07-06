<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a RAG API with FastAPI

**Project Link:** [View Project](http://nextwork.ai/projects/ai-devops-api)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

---

## Introducing Today's Project!

In this project, I'm going to build a local RAG API using FastAPI and ChromaDB. This will help me understand how to load private documents into a vector database, perform semantic search, and generate accurate AI answers locally. I'm interested in this because mastering Retrieval-Augmented Generation allows me to build secure, cost-effective AI assistants tailored to custom datasets.

### Key tools and concepts

I tested my multi-user queries by registering Jordan's profile using the POST endpoint and then querying the GET /ask endpoint with Jordan's username. The filter works because ChromaDB applies a strict metadata filter during search, matching the user parameter to ensure the RAG pipeline only retrieves and references document chunks belonging exclusively to that specific user.

### Challenges and wins

This project took me approximately 2 hours to complete. The most challenging part was resolving Windows-specific environment bottlenecks, which included downgrading to stable Python 3.11 to install precompiled hnswlib C++ binaries, managing active SQLite database file locks, and forcing the pure-Python SegmentAPI engine in ChromaDB to completely bypass silent Rust-compiled core deadlocks during document ingestion.

---

## Performing RAG Manually

In this step, I'm going to set up my local Python project with a virtual environment, install dependencies like FastAPI and ChromaDB, and pull the nomic-embed-text embedding model. RAG stands for Retrieval-Augmented Generation, which is an AI pipeline that retrieves relevant context from documents and uses it to augment the prompt so an LLM can generate accurate, grounded answers.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-devops-api_v3j7x5b9)

### Understanding the three parts of RAG

I performed RAG manually by first asking a question directly to the local LLM to observe a generic or inaccurate response, manually finding the relevant facts in my profile document, and then pasting those facts directly into a new prompt alongside my question to get a grounded, accurate answer. The three parts of this process are Retrieval (searching and finding the relevant text), Augmentation (combining the retrieved context with the user query into a structured prompt), and Generation (submitting the enriched prompt to the model to produce the final response).

### Comparing the two AI models

The key difference I noticed is that nomic-embed-text is an embedding model designed to convert text into mathematical vectors so we can perform search based on meaning, whereas qwen2.5:0.5b is a generative chat model designed to understand a prompt and write conversational answers. In a RAG pipeline, the embedding model acts as the search engine to find relevant context, and the chat model reads that context to generate the final response.

---

## Building a Personal Knowledge Base

In this step, I'm going to write a personal profile document and build a Python script to load, chunk, and store it. Embeddings are numerical vector representations of text that capture its semantic meaning, allowing a vector database like ChromaDB to perform semantic search to find the most relevant context for a question instead of relying on exact keyword matches.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-devops-api_g3h7m2r5)

### Creating the profile document

I included information about my background, current learning goals in cloud computing, and my target career as an AI or DevOps engineer. This custom context will be converted into vector embeddings and stored in ChromaDB. When I query the API, the RAG pipeline will retrieve this specific data to augment the prompt, enabling qwen2.5:0.5b to generate accurate, personalized answers about my skills and experience rather than hallucinating or giving generic responses.

### How semantic search finds relevant chunks

When I ask a question, ChromaDB converts my question into a vector embedding using the same embedding model that processed the profile. It then compares this vector against the stored document vectors and calculates which chunks are mathematically closest in high-dimensional space. Through this semantic search, it retrieves the chunks with the most similar meaning, rather than just matching exact keywords.

---

## Creating the RAG API with FastAPI

In this step, I'm going to build an API that implements a complete RAG pipeline by creating a FastAPI application with a custom GET endpoint. This endpoint will query ChromaDB for context, construct an augmented prompt, and generate answers using Ollama. I'll test it using Swagger UI, an interactive API playground that allows me to execute questions directly in my browser and verify the grounded responses.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-devops-api_j5m1r8t2)

### How the /ask endpoint works

When a question comes in, my endpoint first retrieves the top two most relevant document chunks from ChromaDB using semantic search. Second, it augments the prompt by combining those retrieved chunks with the original question into a structured template. Finally, it generates a grounded response by sending this context-rich prompt to the local qwen2.5:0.5b model via Ollama before returning the final answer and context back to the user.

### Testing with Swagger UI

I tested my API by asking "What is my name?". The AI answered with "Hello! Your full name as provided by Qwen is \"Marc.\" You are a name used in various contexts like on social media or for educational purposes.", accurately identifying me rather than making up a generic response. The context used was a semantic chunk retrieved from ChromaDB containing my personal biography details from my profile, which was passed by FastAPI to augment the prompt before Ollama generated the final response.

---

## Extending to a Multi-User AI Directory

In this project extension, I'm adding multi-user support because it allows a single deployment of my API to securely serve multiple individuals without crossing their private data. Multi-tenancy means partitioning a shared database so that different users, or tenants, are completely isolated from one another. By updating my FastAPI endpoints and using ChromaDB metadata filtering, I can ensure that when a user asks a question, the RAG pipeline only retrieves and references document chunks belonging to their specific profile.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-devops-api_d5g9k3n7)

### Adding the POST /documents endpoint

In this project extension, I added a POST endpoint that allows new users to dynamically register and upload their private biographies to the shared database. Metadata filtering allows my FastAPI code to query ChromaDB using a specific user filter, ensuring that the retrieved document chunks are completely isolated. This guarantees that when a tenant asks a question, the RAG pipeline only retrieves and references context belonging exclusively to their profile.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-devops-api_r8t2w6y1)

### Verifying multi-user filtering

I tested multi-user queries by registering a profile for a new user named Jordan using the POST endpoint, then querying the API with Jordan's username. The filter works because ChromaDB applies a strict metadata filter matching the username parameter during the search, which successfully isolates Jordan's vector embeddings and document chunks from other users' data and ensures the local AI is only supplied with context belonging to that specific tenant.

---

## Wrapping Up

I did this project today to learn how to build and deploy a secure local RAG pipeline programmatically using FastAPI, ChromaDB, and Ollama to search and query my own profile. Another skill I want to learn is containerizing my completed application using Docker and deploying it using automated CI/CD pipelines to build professional DevOps experience.

---

---
