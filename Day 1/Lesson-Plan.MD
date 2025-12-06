# 📘 **Day 1 Lesson Plan — Foundations & Document Pipeline**

### *Building AI Applications with Gemini API & LangChain – 3-Day Crash Course*

---

# **🕒 Total Duration: 3.5 – 4 hours (Lecture + Demo)

🧪 + 1.5 – 2 hours (Lab)**

---

# --------------------------------------------------

# **🔶 Section 1 — Welcome & Orientation (15 min)**

# --------------------------------------------------

### **Learning Objectives**

* Introduce the course structure
* Clarify technical requirements
* Show final capstone app to motivate students

### **Activities**

* Instructor introduces self
* Explain what students will build (RAG + Tools + UI + Deployment)
* Walk through the 3-day roadmap
* Show sample output of final AI assistant

### **Materials**

* Slides 1–4
* Demo capstone app (optional)

---

# --------------------------------------------------

# **🔶 Section 2 — Gemini & LangChain Architecture (20 min)**

# --------------------------------------------------

### **Learning Objectives**

* Understand the roles of Gemini and LangChain
* Understand how embeddings & retrieval work
* Understand the RAG architecture students will implement

### **Key Concepts**

* Gemini = LLM, embeddings, vision
* LangChain = Orchestration (chains, tools, agents)
* Vector DB = memory for document search

### **Activities**

* Diagram walkthrough
* Discuss why RAG > fine-tuning for most business use cases

### **Materials**

* Slides 5–8

---

# --------------------------------------------------

# **🔶 Section 3 — Environment Setup (25 min)**

# --------------------------------------------------

### **Learning Objectives**

* Set up project folder
* Install dependencies
* Configure Gemini API key
* Test first Gemini call

### **Instructor Demo**

1. Clone or create the project structure
2. Show `config.py` and `.env` setup
3. Install requirements
4. Test Gemini connection in Python REPL

### **Student Exercise**

* Students run the same steps on their machine

### **Materials**

* Slides 9–10
* Lab Part 1

---

# --------------------------------------------------

# **🔶 Section 4 — Document Loading (30 min)**

# --------------------------------------------------

### **Learning Objectives**

* Introduce document loaders
* Explore different file formats
* Load PDF & text files into LangChain

### **Instructor Demo**

* Explain loaders: PyPDFLoader, TextLoader
* Load sample documents inside the `documents/` folder
* Show output structure (`Document` objects, metadata)

```python
docs = load_docs()
print("Loaded:", len(docs))
```

### **Student Exercise**

* Students place their own PDFs into `documents/`
* Run loader
* Inspect first document

### **Materials**

* Slides 11
* Lab Part 2

---

# --------------------------------------------------

# **🔶 Section 5 — Chunking & Text Splitting (35 min)**

# --------------------------------------------------

### **Learning Objectives**

* Understand why chunking is necessary
* Test different chunk sizes
* Modify chunking behaviour based on document type

### **Instructor Demo**

* Explain chunk size, overlap
* Show RecursiveCharacterTextSplitter
* Visualize how a large PDF is split

```python
splitter = RecursiveCharacterTextSplitter(
    chunk_size=700,
    chunk_overlap=150
)
chunks = splitter.split_documents(docs)
```

### **Discussion**

* When to use smaller chunks
* When to use larger chunks

### **Student Exercise**

* Students experiment with chunk_size: 200 vs 1500
* Compare number of chunks

### **Materials**

* Slides 12–13
* Lab Part 3

---

# --------------------------------------------------

# **🔶 Section 6 — Embeddings with Gemini (30 min)**

# --------------------------------------------------

### **Learning Objectives**

* Understand semantic embeddings
* Generate embeddings manually
* Discuss embedding use-cases

### **Instructor Demo**

* Show vector representation
* Explain cosine similarity
* Demonstrate embedding a simple query string

```python
emb = GoogleGenerativeAIEmbeddings(model="models/embedding-001")
emb.embed_query("Hello world!")
```

### **Student Exercise**

* Students embed 3–5 sentences
* Compare vector differences

### **Materials**

* Slides 14–15
* Lab Part 4

---

# --------------------------------------------------

# **🔶 Section 7 — Building the Vector Store (35 min)**

# --------------------------------------------------

### **Learning Objectives**

* Build and persist a Chroma vector DB
* Understand how documents are stored & retrieved
* Test querying with similarity search

### **Instructor Demo**

* Walk through code in `vector_store.py`
* Build vector DB and inspect folder
* Show retrieval results

### **Key Code**

```python
build_vectorstore()
vs = get_vectorstore()
vs.similarity_search("What is this document about?")
```

### **Student Exercise**

* Students run builder
* Perform similarity search on their own documents

### **Materials**

* Slides 16–18
* Lab Part 5 & 6

---

# --------------------------------------------------

# **🔶 Section 8 — Day 1 Summary & Milestone (10 min)**

# --------------------------------------------------

### Students Achieved:

✔ Gemini setup
✔ Document ingestion
✔ Chunking pipeline
✔ Embeddings
✔ Vector store
✔ Working similarity search

This completes the backend for RAG.

---

# --------------------------------------------------

# **🔶 Section 9 — Day 1 Lab (90–120 min)**

# --------------------------------------------------

Students complete the full **Day 1 Lab**:

**Lab Tasks**

1. Configure Gemini API
2. Load documents
3. Create chunks
4. Generate embeddings
5. Build Chroma DB
6. Run query retrieval
7. Stretch challenges (optional)

**Instructor Role**

* Rotate to help students debug
* Demonstrate common fixes
* Validate vector DB outputs

**Materials**

* Day 1 Lab document
* Slides 21–23

---

# --------------------------------------------------

# **🔶 Homework (Optional)**

# --------------------------------------------------

1. Add more documents
2. Tune chunk_size and overlap
3. Try an alternative embedding model
4. Add metadata (titles, filenames)

---

# ✔️ **Day 1 Complete**

Students now have a working document→embedding→retrieval pipeline.

