# **Day 2 Slide Deck — RAG, Tools, & Agents**

---

## **Slide 1 — Title Slide**

**Title:** Day 2 — Building Intelligent AI with RAG, Tools & Agents
**Subtitle:** Gemini API + LangChain Crash Course
**Visual:** Diagram of AI pipeline (User → Retriever → LLM → Answer)
**Notes:**

* Welcome learners
* Recap Day 1: Documents loaded, chunked, embedded, vector store ready

---

## **Slide 2 — Objectives**

**Slide Content:**

* Understand Retrieval-Augmented Generation (RAG)
* Build a RAG chain with Gemini + LangChain
* Integrate tools to extend AI capabilities
* Create agents for multi-step reasoning
* Test AI queries with sources

**Visual:** Checklist icon with bullets
**Notes:** Emphasize **Day 2 builds on Day 1 foundation**

---

## **Slide 3 — Recap of Day 1**

**Content:**

* Document Loading: PDFs, TXT → LangChain Documents
* Chunking: RecursiveCharacterTextSplitter → chunks with overlap
* Embeddings: Gemini Embeddings → vector representation
* Vector Store: Chroma → semantic search

**Visual:** Diagram of pipeline

* Documents → Chunking → Embeddings → Vector Store

**Notes:** Set stage for retrieval + generation

---

## **Slide 4 — What is RAG?**

**Content:**

* RAG = Retrieval + Generation
* Steps:

  1. Retrieve relevant chunks from vector store
  2. Feed chunks into LLM
  3. Generate answer with context
* Advantages:

  * Accurate answers
  * Scales to large corpora
  * No fine-tuning required

**Visual:** Flowchart of User Query → Retriever → LLM → Answer

---

## **Slide 5 — Building a RAG Chain**

**Content:**

* **Retriever:** Finds relevant chunks (`vectordb.as_retriever()`)
* **LLM:** Gemini API (`ChatGoogleGenerativeAI`)
* **Chain:** `RetrievalQA` combines retriever + LLM

**Code Snippet:** Short example of `RetrievalQA` creation
**Notes:** Demo: Run a query and show top source documents

---

## **Slide 6 — Tools for AI**

**Content:**

* Extend AI beyond retrieval
* Examples:

  * Calculator
  * Web search API
  * Translation tool
* LangChain `Tool` class: name, function, description

**Visual:** Diagram showing LLM + Tool → Answer
**Code Snippet:** Calculator Tool

---

## **Slide 7 — Multi-step Reasoning with Agents**

**Content:**

* Agents = LLM + Tools + Reasoning
* LangChain agent types:

  * `ZERO_SHOT_REACT_DESCRIPTION`
  * `SELF_ASK_WITH_SEARCH`
* Agents choose tools **autonomously**
* Steps:

  1. Receive query
  2. Determine tool needed
  3. Execute tool
  4. Generate final answer

**Visual:** Flowchart: Query → Agent → Tool → LLM → Answer

---

## **Slide 8 — Demo: RAG + Agent**

**Content / Demo Plan:**

1. Query vector store with RAG chain
2. Ask agent to perform calculation
3. Combine RAG + Agent query

**Visual:** Screenshot placeholder for terminal output
**Notes:**

* Show verbose reasoning
* Show source documents returned

---

## **Slide 9 — Best Practices**

**Content:**

* Return source documents for transparency
* Use chunk overlap for context retention
* Modularize tools for easy extension
* Test agents carefully to avoid unintended tool execution

**Visual:** Checklist or caution icon

---

## **Slide 10 — Lab Exercises**

**Content:**

* Load persisted vector store
* Build RAG chain & test query
* Create calculator tool
* Initialize agent & run multi-step query
* Optional: Add more tools

**Visual:** Table or checklist
**Notes:** Encourage hands-on experimentation

---

## **Slide 11 — Common Errors & Troubleshooting**

**Content / Table:**

| Error                          | Fix                                      |
| ------------------------------ | ---------------------------------------- |
| RAG returns irrelevant results | Increase `k`, check chunk size & overlap |
| Agent fails to call tool       | Check Tool initialization                |
| ModuleNotFoundError            | Run `pip install -r requirements.txt`    |

**Visual:** Warning icon

---

## **Slide 12 — Summary & Takeaways**

**Content:**

* RAG allows context-aware responses
* Tools extend LLM capabilities
* Agents enable multi-step reasoning
* Day 2 prepares backend for **frontend integration on Day 3**

**Visual:** Diagram of full pipeline with RAG + Tools + Agents

---

## **Slide 13 — Next Steps**

**Content:**

* Day 3: Frontend UI, deployment, and full AI assistant
* Prepare your vector store and agent code
* Optional: Experiment with multiple tools

**Visual:** Roadmap timeline: Day 1 → Day 2 → Day 3

---

✅ **Notes for Presenter:**

* Include live coding demos for RAG and agent
* Keep code snippets short; show terminal output
* Encourage learners to ask questions about **tool integration and reasoning**

---

