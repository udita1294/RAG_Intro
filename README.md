# Simple RAG

A simple Retrieval-Augmented Generation (RAG) project built with **Python, Groq, and Llama 3.3 70B**.

This project demonstrates the basic RAG workflow:

1. Store information in a knowledge base.
2. Retrieve relevant information based on the user's question.
3. Pass the retrieved context to an LLM.
4. Generate an answer using only the provided context.

## Project Overview

The project contains a small knowledge base containing information about Udita, such as age and net worth.

When a user asks a question, the program:

```text
User Question
      ↓
Retrieve Relevant Information
      ↓
Knowledge Base
      ↓
Retrieved Context
      ↓
Groq LLM
      ↓
Final Answer
```

## Technologies Used

* **Python**
* **Groq API**
* **Llama 3.3 70B Versatile**
* **python-dotenv**
* Basic RAG concepts

## Project Structure

```text
simple-rag/
│
├── main.py
├── .env
├── .gitignore
└── README.md
```

## How It Works

### Step 1: Knowledge Base

The project starts with a simple dictionary containing information:

```python
knowledge_base = {
    "age": "The age of Udita is 22 years",
    "net worth": "The net worth of Udita is 2000000"
}
```

In a real RAG application, this could be replaced by information stored in:

* PDFs
* Documents
* Databases
* Vector databases
* Websites
* Company knowledge bases

### Step 2: Retrieval

The `retrieve_info()` function checks the question and retrieves relevant information.

```python
def retrieve_info(question):
    question = question.lower()

    if "age" in question:
        return knowledge_base["age"]

    elif "net worth" in question:
        return knowledge_base["net worth"]

    else:
        return None
```

For example:

```text
"What is Udita's age?"
```

returns:

```text
"The age of Udita is 22 years"
```

### Step 3: Generation

The retrieved information is passed to the Groq LLM as context.

The system prompt instructs the model to:

* Answer in one line.
* Use only the provided context.
* Avoid hallucinating information.

```python
sys_prompt = f"""
answer in one line only.
Answer only based on this context.
do not hallucinate.
Context: {context}
"""
```

### Step 4: Final Answer

The question and context are sent to the Groq API using the Llama 3.3 70B model.

```python
response = client.chat.completions.create(
    model=model,
    messages=messages
)
```

The generated answer is then printed.

## Running the Project

Run:

```bash
python main.py
```

Expected output:

```text
Udita is 22 years old.
```

## Example Queries

The current retrieval system can answer questions related to:

```text
What is Udita's age?
```

```text
Tell me Udita's net worth.
```

If the requested information is not available in the knowledge base, the retrieval function returns `None`.

## RAG Architecture

This project demonstrates the fundamental architecture of a RAG system:

```text
                  ┌─────────────────┐
                  │  User Question  │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │    Retriever    │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │ Knowledge Base  │
                  └────────┬────────┘
                           │
                     Retrieved Context
                           │
                           ▼
                  ┌─────────────────┐
                  │    Groq LLM     │
                  │ Llama 3.3 70B   │
                  └────────┬────────┘
                           │
                           ▼
                  ┌─────────────────┐
                  │      Answer     │
                  └─────────────────┘
```

## Current Limitations

This is a **basic RAG implementation** intended for learning purposes.

The retriever currently uses simple keyword matching:

```python
if "age" in question:
```

It does not yet use:

* Embeddings
* Vector databases
* Semantic search
* Document chunking
* Similarity search
* Reranking

## Future Improvements

This project can be extended into a complete RAG application by adding:

### 1. Document Loading

Load information from:

```text
PDF → Text
DOCX → Text
Websites → Text
TXT → Text
```

### 2. Text Chunking

Split large documents into smaller chunks.

```text
Document
   ↓
Chunks
   ↓
Embeddings
```

### 3. Embeddings

Convert text into numerical vectors using an embedding model.

### 4. Vector Database

Store embeddings in a vector database such as:

* FAISS
* ChromaDB
* Pinecone
* Weaviate

### 5. Semantic Retrieval

Instead of keyword matching, retrieve documents based on semantic similarity.

### 6. Improved RAG Pipeline

The final architecture could become:

```text
Documents
    ↓
Document Loader
    ↓
Text Chunking
    ↓
Embeddings
    ↓
Vector Database
    ↓
Similarity Search
    ↓
Relevant Context
    ↓
Groq / Llama
    ↓
Final Answer
```

## Learning Objectives

This project helps understand the basic concepts of:

* Retrieval-Augmented Generation (RAG)
* Prompt engineering
* Context injection
* LLM hallucination prevention
* Information retrieval
* Groq API integration
* Environment variable management
