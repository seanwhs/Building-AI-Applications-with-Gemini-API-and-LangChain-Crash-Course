# **Slide 1 — Title**

## **Day 1: Foundations & Document Ingestion**

**Course:** Building AI Applications with Gemini API & LangChain
**Instructor:** *Your Name Here*
**Goal Today:** Build the foundation for a RAG system

---

# **Slide 2 — Agenda**

1. Course Orientation
2. Gemini + LangChain Architecture
3. Development Environment Setup
4. Document Loading
5. Chunking Strategies
6. Embeddings with Gemini
7. Vector Store (Chroma)
8. Retrieval Test
9. Day 1 Milestone

---

# **Slide 3 — Course Roadmap (3 Days)**

**Day 1:** Foundations + Vector DB
**Day 2:** RAG + Tools + Agents
**Day 3:** UI + Deployment + Capstone

---

# **Slide 4 — What We Will Build**

A full **AI Knowledge Assistant** with:

* 📄 Document uploads
* ✂️ Chunking pipeline
* 🧠 Gemini embeddings
* 🔎 Chroma vector store
* 🤖 RAG + tools + agents
* 🖥️ Web UI + Deployment

---

# **Slide 5 — LangChain + Gemini Overview**

**Gemini:**

* Multimodal LLM
* Embeddings
* Structured output
* Function calling

**LangChain:**

* Tooling framework
* Chains
* Agents
* Retrieval pipelines
* Vector store integrations

---

# **Slide 6 — Architecture Diagram (Simple)**

**Documents → Loader → Chunker → Embeddings → Vector DB → Retriever → Gemini LLM → Answer**

---

# **Slide 7 — Architecture Diagram (Detailed)**

**User Query → Retriever → Relevant Chunks → LLM (Gemini) → Final Answer + Citations**

---

# **Slide 8 — Project Folder Structure (Day 1)**

```
backend/
  config.py
  vector_store.py
documents/
README_DAY1.md
```

---

# **Slide 9 — Environment Setup**

1. Install dependencies
2. Create `.env` with `GEMINI_API_KEY=`
3. Test the Gemini API
4. Confirm document folder exists

---

# **Slide 10 — Testing Gemini Connection**

```python
from langchain_google_genai import ChatGoogleGenerativeAI
ChatGoogleGenerativeAI(model="gemini-1.5-pro")
```

Expected: Model object prints ✔

---

# **Slide 11 — Loading Documents**

Use LangChain loaders:

* `PyPDFLoader`
* `TextLoader`
* `UnstructuredLoader`

Code (example):

```python
docs = load_docs()
```

---

# **Slide 12 — Chunking Concepts**

Why chunk documents?

* LLMs must receive **small, relevant** context
* Prevent token overflow
* Improve retrieval quality

**Good settings (starter):**

* `chunk_size = 700`
* `chunk_overlap = 150`

---

# **Slide 13 — Chunking Code Snippet**

```python
splitter = RecursiveCharacterTextSplitter(
    chunk_size=700,
    chunk_overlap=150
)
chunks = splitter.split_documents(docs)
```

---

# **Slide 14 — Gemini Embeddings**

We use:

```
models/embedding-001
```

Embedding size: **768**

Code:

```python
embed = GoogleGenerativeAIEmbeddings(model="models/embedding-001")
```

---

# **Slide 15 — What Is a Vector?**

* Numerical representation of text
* Captures semantic meaning
* Similar meaning → vectors close together

Visualization:
📄 ➝ 🔢🔢🔢 (vector)

---

# **Slide 16 — Chroma Vector DB**

Why Chroma?

* Fast
* Local, persistent
* Good for prototyping
* Works with LangChain by default

---

# **Slide 17 — Building Chroma**

```python
vectordb = Chroma.from_documents(
    documents=chunks,
    embedding=embeddings,
    persist_directory="./chroma_db"
)
```

---

# **Slide 18 — Testing Retrieval**

```python
vs = get_vectorstore()
results = vs.similarity_search("What is this about?")
```

---

# **Slide 19 — What Success Looks Like**

You should see text from your documents in:

```
results[0].page_content
```

This means:
🎉 Your vector DB is functional
🎉 Retrieval works
🎉 Ready for RAG on Day 2

---

# **Slide 20 — Day 1 Milestone**

By end of today, you have:

✔ Loaded documents
✔ Split them into chunks
✔ Generated Gemini embeddings
✔ Created & persisted a vector DB
✔ Successfully queried the DB

This is the **foundation** for your RAG assistant.

---

# **Slide 21 — Day 1 Lab**

Hands-on tasks:

1. API setup
2. Document ingestion
3. Chunking
4. Embedding
5. Vector DB
6. Retrieval

---

# **Slide 22 — Coming Up Tomorrow**

**Day 2: RAG + Tools + Agents**

* Build Retrieval Chain
* Add Citations
* Add Tools + Function Calling
* Create AI Agents
* Optional: Multimodal (Vision)

---

# **Slide 23 — Q&A**

