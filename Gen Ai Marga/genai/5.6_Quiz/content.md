# 5.6 Quiz: RAG & Integration

## 📋 Module Assessment

This quiz covers all topics from Module 5: Building AI Apps.

**Format**: Multiple choice and short answer questions.
**Passing Score**: 70% (21/30 points)
**Time Limit**: 60 minutes

---

## Section 1: LangChain & Vector Databases (6 points)

### Question 1 (2 points)
**What are the two core principles that LangChain enables?**

A) Fast and cheap  
B) Data-aware and agentic  
C) Secure and scalable  
D) Simple and reliable

**Answer**: B

---

### Question 2 (2 points)
**Why do we use vector databases instead of traditional databases for semantic search?**

A) They are faster  
B) They are cheaper  
C) They search by meaning, not just keywords  
D) They store more data

**Answer**: C

---

### Question 3 (2 points)
**Which of the following is NOT a common vector database?**

A) ChromaDB  
B) Pinecone  
C) PostgreSQL (standard)  
D) FAISS

**Answer**: C

---

## Section 2: Embeddings (4 points)

### Question 4 (2 points)
**What is an embedding?**

A) A compressed version of text  
B) A numerical representation of text that captures semantic meaning  
C) A translation of text  
D) An encrypted version of text

**Answer**: B

---

### Question 5 (2 points)
**Which similarity metric is most commonly used in vector search?**

A) Hamming distance  
B) Manhattan distance  
C) Cosine similarity  
D) Levenshtein distance

**Answer**: C

---

## Section 3: RAG (8 points)

### Question 6 (2 points)
**What does RAG stand for?**

A) Rapid API Generation  
B) Retrieval Augmented Generation  
C) Random Access Gateway  
D) Reliable Agent Generator

**Answer**: B

---

### Question 7 (2 points)
**What is the correct order of steps in a RAG pipeline?**

A) Generate → Retrieve → Augment  
B) Augment → Generate → Retrieve  
C) Retrieve → Augment → Generate  
D) Retrieve → Generate → Augment

**Answer**: C

---

### Question 8 (2 points)
**What is the purpose of "chunk overlap" when splitting documents?**

A) To reduce storage costs  
B) To preserve context across chunk boundaries  
C) To make chunks the same size  
D) To remove duplicate information

**Answer**: B

---

### Question 9 (2 points)
**Which text splitting strategy preserves natural document structure?**

A) Fixed-size chunks  
B) Random splitting  
C) RecursiveCharacterTextSplitter  
D) Single-character splitting

**Answer**: C

---

## Section 4: Function Calling (6 points)

### Question 10 (2 points)
**What is the main benefit of function calling in LLMs?**

A) It makes the LLM faster  
B) It allows the LLM to interact with external systems and APIs  
C) It reduces API costs  
D) It improves grammar

**Answer**: B

---

### Question 11 (2 points)
**When an LLM uses function calling, what does it output?**

A) The final answer immediately  
B) Python code to execute  
C) A structured request (JSON) specifying which function to call  
D) A natural language description of what to do

**Answer**: C

---

### Question 12 (2 points)
**In a function calling workflow, who executes the actual function?**

A) The LLM  
B) The vector database  
C) Your application code  
D) The API provider

**Answer**: C

---

## Section 5: Memory & Conversation (3 points)

### Question 13 (3 points)
**Why do LLM applications need a "memory" component?**

A) To store the model weights  
B) To cache API responses  
C) Because LLMs are stateless and don't remember past messages by default  
D) To reduce latency

**Answer**: C

---

## Section 6: PDF Processing (3 points)

### Question 14 (3 points)
**Which library is best for extracting tables from PDFs?**

A) PyPDF  
B) PDFPlumber  
C) TextLoader  
D) ChromaDB

**Answer**: B

---

## Section 7: Short Answer Questions (10 points total)

### Question 15 (5 points)
**Explain the three phases of a RAG system (Index, Retrieval, Generation) in your own words.**

**Sample Answer**:
- **Index Phase**: Load documents, split them into chunks, create embeddings, and store in a vector database (one-time setup)
- **Retrieval Phase**: Convert user query to embedding, search vector database for most similar chunks
- **Generation Phase**: Insert retrieved chunks as context in the prompt, send to LLM to generate an answer based on that context

**Grading Rubric**:
- 2 points: Correctly describes indexing
- 2 points: Correctly describes retrieval
- 1 point: Correctly describes generation

---

### Question 16 (5 points)
**Describe a real-world scenario where you would use both RAG and function calling together.**

**Sample Answer**:
A customer support bot for an e-commerce company. RAG would be used to answer questions about products by retrieving information from the product catalog. Function calling would be used to check order status, process returns, and update customer information in the database.

**Grading Rubric**:
- 2 points: Identifies appropriate use case
- 2 points: Explains RAG component clearly
- 1 point: Explains function calling component

---

## Bonus Questions (Optional, +5 points)

### Bonus 1 (3 points)
**What is "Maximum Marginal Relevance" (MMR) and why is it useful in retrieval?**

**Answer**: MMR is a retrieval strategy that balances relevance with diversity. Instead of just retrieving the most similar documents, it ensures the results are diverse and cover different aspects of the query. This prevents redundant information.

---

### Bonus 2 (2 points)
**Name two challenges specific to parsing PDF documents (vs plain text) and how you would address them.**

**Sample Answer**:
1. **Table extraction**: PDFs often contain tables that are hard to parse as plain text. Solution: Use PDFPlumber or similar libraries with table extraction capabilities.
2. **Multi-column layouts**: Text order can be confusing. Solution: Use PyMuPDF with layout analysis or Unstructured.io for better structure preservation.

---

## Answer Key

| Question | Answer | Points |
|----------|--------|--------|
| 1 | B | 2 |
| 2 | C | 2 |
| 3 | C | 2 |
| 4 | B | 2 |
| 5 | C | 2 |
| 6 | B | 2 |
| 7 | C | 2 |
| 8 | B | 2 |
| 9 | C | 2 |
| 10 | B | 2 |
| 11 | C | 2 |
| 12 | C | 2 |
| 13 | C | 3 |
| 14 | B | 3 |
| 15 | See rubric | 5 |
| 16 | See rubric | 5 |

**Total**: 30 points (35 with bonus)

---

## Additional Practice Questions

### Practice 1
**What would happen if you set chunk_overlap to 0?**

Answer: You might lose context that spans chunk boundaries, leading to incomplete or inaccurate retrievals.

---

### Practice 2
**When should you use the "map_reduce" chain type instead of "stuff"?**

Answer: When you have many documents that won't fit in a single prompt. Map_reduce summarizes each document separately, then combines the summaries.

---

### Practice 3
**What information should you include in a function definition for optimal LLM performance?**

Answer:
- Clear function name
- Detailed description of what it does
- Parameter names with types
- Description for each parameter
- Which parameters are required

---

## Study Resources

### Review These Sections
1. [5.1 Vector Databases](../5.1_Intro_LangChain_VectorDBs/content.md#vector-databases-the-memory-for-ai)
2. [5.2 RAG Workflow](../5.2_RAG/content.md#the-rag-workflow)
3. [5.3 Function Calling](../5.3_AI_API_Integration/content.md#how-it-works)

### Practice Projects
- Rebuild the Movie Search Engine
- Create variations of the Weather Assistant
- Modify the PDF Chatbot

---

**🎉 Congratulations on completing Module 5!**

You now have the skills to build sophisticated AI applications that:
- Access private knowledge bases
- Integrate with external APIs
- Maintain conversational memory
- Handle complex user workflows

**What's Next?**
- Build your own project
- Explore advanced topics (agents, multi-modal AI)
- Deploy your apps to production
