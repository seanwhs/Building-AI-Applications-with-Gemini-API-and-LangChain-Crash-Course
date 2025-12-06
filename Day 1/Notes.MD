# **Day 1 Notes — Foundations & Document Pipeline**

### *Building AI Applications with Gemini API & LangChain*

---

## **1. Introduction & Motivation**

* **Purpose of the Course:** Equip learners to build **intelligent AI applications** that can:

  * Understand documents semantically
  * Retrieve relevant information efficiently
  * Answer user queries contextually
  * Integrate tools and agents in later stages

* **Why Gemini + LangChain?**

  * Gemini: Powerful LLM with embeddings, multimodal capabilities, and function calling
  * LangChain: Flexible orchestration framework for building pipelines, tools, and agents
  * RAG architecture: Combines LLM with retrieval for **scalable, accurate, context-aware AI**

* **Capstone App Demo Highlights (Motivation):**

  * Upload documents (PDFs, text)
  * Ask complex questions
  * Retrieve context from multiple sources
  * Output answers with references

---

## **2. Understanding LLMs, Embeddings, and RAG**

### **2.1 LLMs**

* Language models predict the next token given a context
* Strengths: Generation, reasoning, summarization
* Limitations: Finite context window → cannot process large documents directly

### **2.2 Embeddings**

* Numeric vector representation of text, capturing semantic meaning
* Similar texts → similar vectors (cosine similarity)
* Key use cases:

  * Semantic search
  * Clustering and topic modeling
  * Content recommendation

### **2.3 Retrieval-Augmented Generation (RAG)**

* Combines retrieval and generation:

  1. Retrieve relevant chunks from vector store
  2. Feed them as context to LLM
  3. Generate accurate, context-aware answers
* Advantages over fine-tuning:

  * No need for expensive model training
  * Scales easily with document corpus
  * Handles dynamic content

---

## **3. Project Setup & Architecture**

### **3.1 Project Structure**

```
gemini-langchain-app/
│
├── backend/
│   ├── config.py          # API keys, constants
│   ├── vector_store.py    # Embeddings + vector DB
│   ├── rag.py             # Retrieval + LLM pipeline
│   ├── tools.py           # Optional tools & function calls
│   ├── models.py          # LLM & embeddings initialization
│   └── main.py            # FastAPI backend entry
│
├── frontend/
│   └── app.py             # Streamlit UI
│
├── documents/
│   └── sample.pdf
│
└── README.md
```

### **3.2 Environment**

* Python 3.10+ recommended
* Install dependencies via:

```bash
pip install -r requirements.txt
```

* **API Key Management**: `.env` file:

```
GEMINI_API_KEY=your_api_key_here
```

**Best Practice:** Never hardcode API keys; always use environment variables for security.

---

## **4. Document Loading**

### **4.1 Purpose**

* Load PDFs, TXT, Markdown, or other structured/unstructured files
* Convert to **LangChain Document objects** with metadata

### **4.2 Loaders**

| Loader               | Use Case                 |
| -------------------- | ------------------------ |
| `PyPDFLoader`        | PDF documents            |
| `TextLoader`         | Plain text               |
| `UnstructuredLoader` | Multiple formats, robust |
| `CSVLoader`          | Structured tabular data  |

### **4.3 Code Example**

```python
from langchain.document_loaders import PyPDFLoader, TextLoader

loader = PyPDFLoader("documents/sample.pdf")
docs = loader.load()
print(f"Loaded {len(docs)} pages")
```

### **4.4 Best Practices**

* Always inspect the first few pages of documents
* Normalize text (remove extra whitespace, headers, footers)
* Store metadata (filename, page number) for context in retrieval

---

## **5. Text Splitting / Chunking**

### **5.1 Why Chunk?**

* LLMs have a limited **context window**
* Chunking helps:

  * Prevent context overflow
  * Improve retrieval accuracy
  * Preserve semantic meaning via overlaps

### **5.2 Text Splitters**

* `RecursiveCharacterTextSplitter`:

  * Recursively splits text to match `chunk_size`
  * Maintains `chunk_overlap` for context

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(
    chunk_size=700,
    chunk_overlap=150
)
chunks = splitter.split_documents(docs)
print(f"Created {len(chunks)} chunks")
```

### **5.3 Design Considerations**

* Small chunk_size → fine-grained retrieval, more chunks → more compute
* Large chunk_size → more context per chunk, fewer chunks → risk exceeding context window
* Overlap helps maintain context between chunks

---

## **6. Embeddings**

### **6.1 Concept**

* Embeddings map text to high-dimensional vector space
* Captures meaning, not just keywords
* Useful for:

  * Semantic search
  * Clustering similar content
  * Feeding LLMs with context

### **6.2 Gemini Embeddings**

```python
from langchain_google_genai import GoogleGenerativeAIEmbeddings

embed_model = GoogleGenerativeAIEmbeddings(model="models/embedding-001")
vector = embed_model.embed_query("Hello world")
print(len(vector))  # e.g., 768 dimensions
```

### **6.3 Tips**

* Always normalize text (lowercase, remove extra whitespace)
* Compare vectors with **cosine similarity**
* Embedding dimension choice affects memory & accuracy

---

## **7. Vector Stores**

### **7.1 Purpose**

* Store embeddings for **fast semantic retrieval**
* Examples: Chroma (local), FAISS (fast, scalable), Pinecone (cloud)

### **7.2 Chroma Example**

```python
from langchain.vectorstores import Chroma

vectordb = Chroma.from_documents(
    documents=chunks,
    embedding=embed_model,
    persist_directory="./chroma_db"
)
vectordb.persist()
```

### **7.3 Querying Vector Store**

```python
results = vectordb.similarity_search("Explain AI document processing")
print(results[0].page_content[:400])
```

* Returns **most semantically similar chunks**
* Useful for feeding into LLM during RAG

### **7.4 Design Notes**

* Persist DB to disk for **reproducibility**
* Include metadata in vectors (filename, page number) for **source tracking**
* Monitor memory usage if embedding large corpora

---

## **8. RAG Prep — What Day 1 Achieves**

By end of Day 1:

* **Documents loaded & inspected**
* **Chunks created & overlapped**
* **Embeddings generated**
* **Vector store built & persisted**
* **Similarity search working**

Next step: feed retrieved chunks into **Gemini LLM** for answers (Day 2)

---

## **9. Lab Exercises**

| Lab | Task                           | Key Outcome                     |
| --- | ------------------------------ | ------------------------------- |
| 1   | Setup environment & Gemini API | API key validated               |
| 2   | Load documents                 | Loaded `Document` objects       |
| 3   | Chunk documents                | Chunks created with overlap     |
| 4   | Generate embeddings            | Vector representation of chunks |
| 5   | Build Chroma DB                | Persistent vector store         |
| 6   | Similarity search              | Retrieve relevant chunks        |

**Stretch Tasks:**

* Experiment with chunk sizes (200, 700, 1500)
* Add custom metadata for retrieval context
* Compare FAISS vs Chroma

---

## **10. Common Issues & Troubleshooting**

| Issue                       | Possible Solution                       |
| --------------------------- | --------------------------------------- |
| Module not found            | `pip install -r requirements.txt`       |
| Embeddings fail             | Verify Gemini API key in `.env`         |
| Retrieval returns empty     | Ensure vector store built, check chunks |
| Chunk size too small        | Fewer tokens → increase `chunk_size`    |
| Context lost between chunks | Increase `chunk_overlap`                |

---

## **11. Advanced Insights**

* **Multilingual support:** Gemini embeddings support multiple languages
* **Memory vs accuracy tradeoff:** More chunks → finer granularity, but higher computational cost
* **Metadata usage:** Allows tracing source of retrieved chunks → improves transparency
* **Chunking heuristics:** Can combine `RecursiveCharacterTextSplitter` with `Language-aware Splitters` (e.g., sentence or paragraph boundary detection)
* **Next step (Day 2):** Integrate retrieval with LLM, add **tools and agents**, start RAG pipeline

---

## **12. Key Takeaways**

1. **Foundational pipeline** for AI Knowledge Assistant is built
2. Embeddings + vector store = **semantic memory**
3. Chunking + overlap = **context preservation**
4. Day 1 sets up **retrieval layer** for RAG system
5. Next, integrate with LLM and function tools

---

✅ **End of Day 1 Notes**

---
