# 🧪 **Day 1 Lab — Document Ingestion, Chunking & Vector Database**

### *Building AI Applications with Gemini API & LangChain – Crash Course*

---

# 🎯 **Lab Objectives**

By the end of this lab you will:

1. Set up your Gemini + LangChain environment
2. Load PDF/Text documents
3. Chunk documents using LangChain splitters
4. Generate embeddings using Gemini
5. Build a Chroma vector database
6. Run similarity search to confirm retrieval works

This is the **foundation of your final RAG application**.

---

# 📝 **Prerequisites**

Before starting the lab:

✔ Python 3.10+ installed
✔ Completed Day 1 setup (project created, requirements installed)
✔ Gemini API Key ready
✔ A few PDFs or text documents placed in the `documents/` folder

---

# 📂 **Lab Files Used**

You will work with:

```
backend/
    config.py
    vector_store.py
documents/
```

---

# 🧩 **LAB PART 1 — Configure API + Environment**

### **Step 1 — Create your `.env` file**

Inside `backend/`:

```
GEMINI_API_KEY=YOUR_KEY_HERE
```

### **Step 2 — Verify Gemini access**

Run:

```bash
python - <<EOF
from langchain_google_genai import ChatGoogleGenerativeAI
llm = ChatGoogleGenerativeAI(model="gemini-1.5-pro")
print("Connected:", llm)
EOF
```

**Expected Output:**

```
Connected: ChatGoogleGenerativeAI(...)
```

If you see this → ✔ Gemini access is working.

---

# 📘 **LAB PART 2 — Document Loading**

### **Step 3 — Ensure you have sample documents**

Put at least 1–3 PDFs or text files in:

```
documents/
    sample1.pdf
    manual.pdf
    notes.txt
```

### **Step 4 — Test the loader**

Inside Python:

```bash
python - <<EOF
from vector_store import load_docs
docs = load_docs()
print("Loaded", len(docs), "documents")
print("Sample:", docs[0].page_content[:300])
EOF
```

**Expected Output:**

```
Loaded 3 documents
Sample:  (first few lines of your file)
```

---

# ✂️ **LAB PART 3 — Text Chunking**

### **Step 5 — Try chunking manually**

```bash
python - <<EOF
from langchain.text_splitter import RecursiveCharacterTextSplitter
from vector_store import load_docs

docs = load_docs()

splitter = RecursiveCharacterTextSplitter(
    chunk_size=700,
    chunk_overlap=150
)

chunks = splitter.split_documents(docs)

print("Chunks created:", len(chunks))
print("Chunk Example:\n", chunks[0].page_content[:300])
EOF
```

**Expected Output:**

```
Chunks created: 15
Chunk Example: <first 300 chars>
```

If you get 0 chunks → documents may be too small.

---

# 🧠 **LAB PART 4 — Generate Embeddings with Gemini**

### **Step 6 — Test embeddings**

```bash
python - <<EOF
from langchain_google_genai import GoogleGenerativeAIEmbeddings

embed = GoogleGenerativeAIEmbeddings(model="models/embedding-001")
vec = embed.embed_query("Hello world!")
print("Embedding length:", len(vec))
EOF
```

**Expected:**

```
Embedding length: 768
```

🎉 You now have embedding capabilities.

---

# 💾 **LAB PART 5 — Build the Vector Store**

### **Step 7 — Run the builder**

```bash
python - <<EOF
from vector_store import build_vectorstore
build_vectorstore()
print("Vector store created!")
EOF
```

**Expected:**

```
Vector store created!
```

Check folder:

```
chroma_db/
    chroma.sqlite3
    index/
```

---

# 🔍 **LAB PART 6 — Test Retrieval (Similarity Search)**

### **Step 8 — Ask the database a question**

```bash
python - <<EOF
from vector_store import get_vectorstore

vs = get_vectorstore()
results = vs.similarity_search("What topics are discussed?")
print("Top chunk:\n", results[0].page_content[:400])
EOF
```

**Expected Output:**

Your most relevant chunk should appear. If not, widen your question or try:

```
"What is this document about?"
```

---

# 🎉 **LAB COMPLETED**

At this point your system can:

✔ Load real documents
✔ Split into chunks
✔ Generate embeddings
✔ Persist a vector store
✔ Retrieve relevant chunks

This is the foundation for building **RAG**, which you'll build tomorrow.

---

# 🔧 **Troubleshooting**

### 🚫 *“No module named …”*

Run:

```
pip install -r backend/requirements.txt
```

### 🚫 Embeddings fail

Check `.env` is in `backend/`.

### 🚫 Retrieval returns nothing

Use bigger documents
or verify you called `build_vectorstore()` again.

---

# ⭐ **Stretch Challenge (Optional)**

Try one of these if you finish early:

### **Challenge A:**

Switch from Chroma to FAISS:

```python
from langchain_community.vectorstores import FAISS
```

### **Challenge B:**

Try different chunk sizes:

* `chunk_size=200`
* `chunk_size=2000`

Compare retrieval quality.

### **Challenge C:**

Add metadata (title, filename) to each chunk.

---
