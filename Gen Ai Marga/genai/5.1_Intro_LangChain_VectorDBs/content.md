# 5.1 Introduction to LangChain & Vector Databases

## 📋 Learning Objectives
By the end of this module, you will be able to:
- Understand what LangChain is and why it's useful for AI application development
- Explain the concept of embeddings and vector similarity
- Set up and use a vector database (ChromaDB)
- Build a semantic search application
- Create your first mini-project: Semantic Search Engine

**Estimated Time:** Week 1-2 (10-12 hours)

---

## 📘 Theory Section (50%)

### What is LangChain?

**LangChain** is a framework designed to simplify the creation of applications using large language models (LLMs). Think of it as a toolkit that connects your LLM to the real world.

#### Core Principles
LangChain enables applications that are:

1. **Data-aware**: Your LLM can access external data sources
   - Read from databases
   - Query APIs
   - Process documents
   
2. **Agentic**: Your LLM can interact with its environment
   - Make decisions
   - Use tools
   - Take actions

#### Key Components

```python
# LangChain's main building blocks
from langchain_core.prompts import PromptTemplate
from langchain_openai import ChatOpenAI
from langchain_core.output_parsers import StrOutputParser

# 1. Prompts - Templates for LLM instructions
prompt = PromptTemplate.from_template("Tell me a joke about {topic}")

# 2. Models - The LLM itself
llm = ChatOpenAI(model="gpt-4")

# 3. Output Parsers - Structure the response
parser = StrOutputParser()

# 4. Chains - Connect components together
chain = prompt | llm | parser
result = chain.invoke({"topic": "AI"})
```

### Vector Databases: The Memory for AI

#### What are Embeddings?

**Embeddings** transform text into numbers (vectors) that capture semantic meaning. Similar concepts have similar vectors.

```
"dog" → [0.2, 0.8, 0.1, ...]
"puppy" → [0.19, 0.81, 0.09, ...]  # Very close!
"car" → [0.9, 0.1, 0.05, ...]      # Far away
```

#### Why Vector Databases?

Traditional databases search by keywords:
- Query: "python programming"
- Matches: Documents with exact words "python" AND "programming"

Vector databases search by **meaning**:
- Query: "python programming"
- Matches: Documents about "coding in Python", "Python development", "writing Python scripts"

#### Popular Vector Databases

| Database | Type | Best For |
|----------|------|----------|
| **ChromaDB** | Embedded | Development, small projects |
| **Pinecone** | Cloud | Production, scalable apps |
| **FAISS** | Library | High-performance search |
| **Weaviate** | Self-hosted | Full control, open source |

#### How Vector Search Works

```mermaid
graph LR
    A[User Query: "space movies"] --> B[Convert to Embedding]
    B --> C[Vector: 0.5, 0.2, 0.8...]
    C --> D[Search Vector DB]
    D --> E[Find Similar Vectors]
    E --> F[Return: "Star Wars", "Interstellar"]
```

### Similarity Metrics

Vector databases use mathematical formulas to find "closeness":

1. **Cosine Similarity**: Measures angle between vectors (most common)
2. **Euclidean Distance**: Measures straight-line distance
3. **Dot Product**: Measures alignment

---

## 🧪 Lab Section (50%)

### Lab 1: Setting Up Your Environment

**Objective**: Install LangChain and ChromaDB

```bash
# Create a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install langchain langchain-openai langchain-community chromadb python-dotenv
```

**Create `.env` file**:
```
OPENAI_API_KEY=your_api_key_here
```

### Lab 2: Your First Embedding

**Objective**: Create embeddings and see the magic

```python
# lab_embeddings.py
import os
from dotenv import load_dotenv
from langchain_openai import OpenAIEmbeddings

load_dotenv()

# Initialize embeddings model
embeddings = OpenAIEmbeddings()

# Create embeddings
texts = [
    "The dog is running in the park",
    "A puppy plays with a ball",
    "The car is parked in the garage"
]

# Get vectors
vectors = embeddings.embed_documents(texts)

print(f"Number of embeddings: {len(vectors)}")
print(f"Dimension of each vector: {len(vectors[0])}")
print(f"First vector (truncated): {vectors[0][:5]}...")

# Compare similarity (cosine similarity)
import numpy as np

def cosine_similarity(v1, v2):
    return np.dot(v1, v2) / (np.linalg.norm(v1) * np.linalg.norm(v2))

sim_dog_puppy = cosine_similarity(vectors[0], vectors[1])
sim_dog_car = cosine_similarity(vectors[0], vectors[2])

print(f"\nSimilarity between 'dog' and 'puppy' sentences: {sim_dog_puppy:.4f}")
print(f"Similarity between 'dog' and 'car' sentences: {sim_dog_car:.4f}")
```

**Expected Output**:
```
Similarity between 'dog' and 'puppy' sentences: 0.8234
Similarity between 'dog' and 'car' sentences: 0.3421
```

### Lab 3: Vector Database Basics

**Objective**: Store and retrieve data from ChromaDB

```python
# lab_vectordb.py
from langchain_community.vectorstores import Chroma
from langchain_openai import OpenAIEmbeddings
from dotenv import load_dotenv

load_dotenv()

# Sample documents
documents = [
    "LangChain is a framework for building LLM applications",
    "Vector databases store embeddings for semantic search",
    "Python is a popular programming language",
    "Machine learning models can be trained on large datasets",
    "ChromaDB is an open-source embedding database"
]

# Create embeddings and store in ChromaDB
embeddings = OpenAIEmbeddings()
db = Chroma.from_texts(documents, embeddings)

# Search for similar content
query = "What is a vector database?"
results = db.similarity_search(query, k=2)

print("Query:", query)
print("\nTop Results:")
for i, doc in enumerate(results, 1):
    print(f"{i}. {doc.page_content}")
```

### 🎯 Mini Project 1: Semantic Movie Search Engine

**Objective**: Build a search engine that finds movies by plot description, not just title.

**Requirements**:
1. Store 20+ movie descriptions
2. Allow users to search by describing a plot
3. Return top 3 matches with similarity scores

**Starter Code**:

```python
# movie_search.py
from langchain_community.vectorstores import Chroma
from langchain_openai import OpenAIEmbeddings
from dotenv import load_dotenv

load_dotenv()

# Movie database
movies = [
    "The Shawshank Redemption: Two imprisoned men bond over a number of years, finding redemption through acts of common decency.",
    "The Godfather: The aging patriarch of an organized crime dynasty transfers control to his reluctant son.",
    "The Dark Knight: Batman must accept one of the greatest psychological tests to fight injustice against the Joker.",
    "Inception: A thief who steals corporate secrets through dream-sharing technology is given the inverse task of planting an idea.",
    "The Matrix: A computer hacker learns about the true nature of his reality and his role in the war against its controllers.",
    "Forrest Gump: The presidencies of Kennedy and Johnson unfold through the perspective of an Alabama man with an IQ of 75.",
    "Pulp Fiction: The lives of two mob hitmen, a boxer, and a pair of diner bandits intertwine in four tales of violence.",
    "The Lord of the Rings: A meek Hobbit and eight companions set out on a journey to destroy the One Ring.",
    "Interstellar: A team of explorers travel through a wormhole in space to ensure humanity's survival.",
    "The Silence of the Lambs: A young FBI cadet must confide in an incarcerated cannibal killer to catch another serial killer.",
]

# TODO: Initialize embeddings and vector store
embeddings = OpenAIEmbeddings()
db = Chroma.from_texts(movies, embeddings)

def search_movies(query, k=3):
    """Search for movies matching the query."""
    # TODO: Implement similarity search with scores
    results = db.similarity_search_with_score(query, k=k)
    return results

# Test the search
if __name__ == "__main__":
    print("🎬 Semantic Movie Search Engine\n")
    
    while True:
        user_query = input("Describe a movie plot (or 'quit' to exit): ")
        if user_query.lower() == 'quit':
            break
            
        results = search_movies(user_query)
        
        print(f"\n🔍 Top {len(results)} matches for: '{user_query}'\n")
        for i, (doc, score) in enumerate(results, 1):
            # Lower score = more similar in ChromaDB
            similarity_percent = (1 - score) * 100
            print(f"{i}. [{similarity_percent:.1f}% match] {doc.page_content[:80]}...")
        print()
```

**Extension Challenges**:
1. Add movie titles and years as metadata
2. Allow filtering by genre
3. Store the database persistently (use `persist_directory`)
4. Add more movies (100+) from a CSV file

---

## 📚 Resources & References

### Official Documentation
- [LangChain Documentation](https://python.langchain.com/docs/get_started/introduction)
- [ChromaDB Documentation](https://docs.trychroma.com/)
- [OpenAI Embeddings Guide](https://platform.openai.com/docs/guides/embeddings)

### Additional Reading
- "What are embeddings?" - [OpenAI Blog](https://openai.com/blog/introducing-text-and-code-embeddings)
- "Vector Database Primer" - [Pinecone Learning Center](https://www.pinecone.io/learn/)

### Video Tutorials
- LangChain Crash Course (YouTube)
- Understanding Vector Databases (YouTube)

---

## ✅ Knowledge Check

Before moving to the next module, ensure you can:
- [ ] Explain what LangChain is in your own words
- [ ] Describe how embeddings represent semantic meaning
- [ ] Create and query a vector database
- [ ] Complete the Movie Search mini-project
- [ ] Explain the difference between keyword and semantic search

---

**Next Module**: [5.2 RAG (Retrieval Augmented Generation)](../5.2_RAG/content.md)
