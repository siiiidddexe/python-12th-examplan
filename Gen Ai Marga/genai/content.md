# Building AI Apps

Welcome to Module 5: Building AI Apps. This module focuses on moving beyond simple prompts to building robust, data-aware applications using LLMs.

**Course Pattern:** 50% Theory, 50% Lab.
**Goal:** Build a "Support Bot with Memory" by the end of this module.

---

## 5.1 Intro to LangChain & Vector DBs

### 📘 Theory (50%)
**LangChain** is a framework for developing applications powered by language models. It enables applications that are:
- **Data-aware**: Connect a language model to other sources of data.
- **Agentic**: Allow a language model to interact with its environment.

**Vector Databases (Vector DBs)** store data as high-dimensional vectors (embeddings). This allows for semantic search—finding text that means the same thing, not just matching keywords.
- *Key Concepts*: Embeddings, Similarity Search, Pinecone/ChromaDB/FAISS.

### 🧪 Lab (50%)
**Setup**: Install `langchain`, `langchain-openai`, `chromadb`.

**Mini Project 1: Semantic Search Engine**
Create a script that stores a list of movie descriptions in a Vector DB and finds the best match for a user's query.

```python
# pseudo-code for lab
from langchain_community.vectorstores import Chroma
from langchain_openai import OpenAIEmbeddings

documents = ["A movie about space war", "A movie about love in Paris"]
db = Chroma.from_texts(documents, OpenAIEmbeddings())
results = db.similarity_search("Science fiction battle")
print(results[0].page_content)
```

---

## 5.2 RAG (Retrieval Augmented Generation)

### 📘 Theory (50%)
**RAG** optimizes the output of an LLM, so it references an authoritative knowledge base outside its training data before generating a response.
1.  **Retrieve**: Find relevant documents from the Vector DB based on the user query.
2.  **Augment**: Insert those documents into the prompt as context.
3.  **Generate**: The LLM answers the question using the provided context.

### 🧪 Lab (50%)
**Exercise**: Build a simple RAG pipeline.
1.  Load a text file.
2.  Split it into chunks.
3.  Store in Vector DB.
4.  Retrieve and answer a question.

---

## 5.3 Integrating AI with existing APIs

### 📘 Theory (50%)
LLMs are "brains" in a jar. To be useful, they need hands. **Function Calling** (or Tool Use) allows LLMs to interact with external APIs (Weather, Stocks, CRM).
- The LLM outputs structured JSON to call a function instead of text.
- Your code executes the function and feeds the result back to the LLM.

### 🧪 Lab (50%)
**Mini Project 2: Smart Weather Assistant**
Build a CLI tool where the user asks "What's the weather in NY?" and the AI calls a mock weather API to give the answer.

```python
# pseudo-code for lab
tools = [weather_tool]
llm_with_tools = llm.bind_tools(tools)
response = llm_with_tools.invoke("Weather in NY?")
# Execute tool and return response
```

---

## 5.4 Examples: Chat with PDF

### 📘 Theory (20%)
Applying RAG to PDF documents involves specific challenges: parsing PDF structure, handling tables, and chunking effectively.

### 🧪 Lab (80%)
**Mini Project 3: PDF Chatbot**
Build a Streamlit or CLI app that allows users to upload a PDF and ask questions about it.
- Use `PyPDFLoader` to extract text.
- Use `RecursiveCharacterTextSplitter` for chunking.
- Implement a conversational retrieval chain.

---

## 5.5 Project: Support Bot with Memory

### 🚀 Main Major Project
**Objective**: Build a Customer Support Bot for a fictional tech company "TechNova".

**Features**:
1.  **Knowledge Base**: Index the "TechNova Product Manual" (a text/PDF file) using RAG.
2.  **Memory**: The bot must remember the user's name and previous questions in the conversation (using `ConversationBufferMemory` or similar).
3.  **Tools**: Give the bot a "CheckOrderStatus" tool to look up order details by ID.

**Steps**:
1.  **Ingest Data**: Load manual into Vector DB.
2.  **Define Tools**: Create `check_order_status(order_id)`.
3.  **Setup Agent**: Initialize an Agent with RAG tool + Order tool + Memory.
4.  **UI**: Create a simple loop or web interface for the chat.

---

## 5.6 Quiz: RAG & Integration

### 📝 Assessment (5 Quizzes)

**Q1: Embeddings**
What is the primary purpose of "Embeddings" in a Vector DB?
A) To compress text data.
B) To represent text as numbers capturing semantic meaning.
C) To translate text into different languages.

**Q2: RAG Workflow**
Which order is correct for a RAG pipeline?
A) Generate -> Retrieve -> Augment
B) Augment -> Generate -> Retrieve
C) Retrieve -> Augment -> Generate

**Q3: Vector Stores**
Which of the following is NOT a common Vector Database?
A) Pinecone
B) ChromaDB
C) MySQL (Standard)
D) FAISS

**Q4: Function Calling**
When an LLM uses "Function Calling", what does it output?
A) The final answer immediately.
B) Python code to be run.
C) A structured request (e.g., JSON) specifying which function to call and with what arguments.

**Q5: Memory**
Why do standard LLM API calls need a "Memory" component?
A) Because LLMs are stateless and don't remember past requests by default.
B) To store the model weights.
C) To make the API cheaper.

---
*End of Module 5 Content*
