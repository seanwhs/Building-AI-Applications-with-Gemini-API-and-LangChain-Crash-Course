# 📘 **Day 1 – README: Foundations & Document Ingestion**

### *Building AI Applications with Gemini API & LangChain – 3-Day Crash Course*

Welcome to **Day 1**!
Today you will set up your development environment, understand the core architecture of Gemini + LangChain apps, and build the first major milestone of your final project:

> **By the end of Day 1, you will have a working system that loads documents, chunks them, embeds them, and stores them in a vector database (Chroma).**

This forms the foundation of your full RAG (Retrieval-Augmented Generation) assistant.

---

# 🧩 **Day 1 Learning Objectives**

### ✔ Understand how Gemini integrates with LangChain

### ✔ Set up project environment, keys, and folder structure

### ✔ Load PDFs/text files into LangChain

### ✔ Chunk documents intelligently

### ✔ Generate embeddings using Gemini

### ✔ Build & persist a vector store using Chroma

### ✔ Test retrieval through similarity search

---

# 📁 **Project Structure (Day 1 Version)**

Today we work inside only these files:

```
backend/
    config.py
    vector_store.py
documents/
README_DAY1.md
```

The rest will be added on Days 2 and 3.

---

# 🛠️ **1. Environment Setup**

### **Install Python dependencies**

From the `backend/` folder run:

```bash
pip install -r requirements.txt
```

### **Add your API key**

Create a `.env` file inside `backend/`:

```
GEMINI_API_KEY=your_key_here
```

Validate:

```bash
python - <<EOF
from langchain_google_genai import ChatGoogleGenerativeAI
print(ChatGoogleGenerativeAI(model="gemini-1.5-pro"))
EOF
```

If you see a model object printed: **success** 🎉

---

# 📑 **2. Add Documents**

Place your PDFs or text files inside the `documents/` folder, for example:

```
documents/
   intro.pdf
   manual.pdf
   notes.txt
```

These will be automatically detected.

---

# 🧠 **3. Chunking, Embeddings & Vector Store**

Open:

```
backend/vector_store.py
```

This script:

1. Loads all documents
2. Splits them into chunks using **RecursiveCharacterTextSplitter**
3. Generates embeddings using **Gemini embeddings**
4. Stores them in a **Chroma** vector database

### Run the builder:

```bash
python - <<EOF
from vector_store import build_vectorstore
build_vectorstore()
print("Vector store created!")
EOF
```

You should now see:

```
chroma_db/
    chroma.sqlite3
    index/
```

---

# 🔍 **4. Test Retrieval**

Run:

```bash
python - <<EOF
from vector_store import get_vectorstore
vs = get_vectorstore()
results = vs.similarity_search("What is this document about?")
print(results[0].page_content)
EOF
```

If you see text from your documents → Retrieval is working.

---

# 🚧 **Troubleshooting**

### **Error: No API key found**

Check `.env` is in `backend/` and you reloaded your shell.

### **Error: “No module langchain_google_genai”**

Install the missing dependencies:

```bash
pip install langchain-google-genai
```

### **Empty results during retrieval**

Ensure:

* Your documents aren’t too short
* You re-ran `build_vectorstore()` after adding new files

---

# 🎯 **Day 1 Milestone Achieved!**

At this point, your system can:

✔ Load documents
✔ Chunk them
✔ Embed them using Gemini
✔ Persist embeddings using Chroma
✔ Perform vector retrieval

This is the **brains** of your final RAG application.

---

# 📅 **What’s Coming on Day 2**

Tomorrow you will build:

🚀 Full RAG chain (retrieval + LLM answer + citations)
🚀 Tool augmentation & agents
🚀 Optional multimodal enhancements (vision)
🚀 Backend API (FastAPI)

This will turn your embeddings into a true **AI Assistant**.

