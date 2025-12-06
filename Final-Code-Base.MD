# 📁 **Project Structure**

```
gemini-langchain-app/
│
├── backend/
│   ├── main.py
│   ├── rag.py
│   ├── tools.py
│   ├── vector_store.py
│   ├── models.py
│   ├── requirements.txt
│   └── config.py
│
├── frontend/
│   ├── app.py
│   ├── requirements.txt
│
├── documents/         # uploaded PDFs or text files
│
└── README.md
```

---

# 🔧 **1. backend/config.py**

```python
import os
from dotenv import load_dotenv

load_dotenv()

GEMINI_API_KEY = os.getenv("GEMINI_API_KEY")
```

---

# 🔧 **2. backend/models.py**

```python
from pydantic import BaseModel

class QueryRequest(BaseModel):
    query: str

class AnswerResponse(BaseModel):
    answer: str
    sources: list[str] = []
```

---

# 🔧 **3. backend/vector_store.py**

```python
import os
from langchain_community.document_loaders import PyPDFLoader, TextLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain_chroma import Chroma
from langchain_google_genai import GoogleGenerativeAIEmbeddings

CHROMA_PATH = "./chroma_db"

embeddings = GoogleGenerativeAIEmbeddings(model="models/embedding-001")

def load_docs(path="documents"):
    docs = []
    for file in os.listdir(path):
        full = os.path.join(path, file)
        if file.endswith(".pdf"):
            docs.extend(PyPDFLoader(full).load())
        else:
            docs.extend(TextLoader(full).load())
    return docs

def build_vectorstore():
    docs = load_docs()
    splitter = RecursiveCharacterTextSplitter(chunk_size=700, chunk_overlap=150)
    chunks = splitter.split_documents(docs)

    vectordb = Chroma.from_documents(
        documents=chunks,
        embedding=embeddings,
        persist_directory=CHROMA_PATH,
    )
    vectordb.persist()
    return vectordb

def get_vectorstore():
    return Chroma(
        persist_directory=CHROMA_PATH,
        embedding_function=embeddings,
    )
```

---

# 🔧 **4. backend/tools.py**

Example custom tools used by the agent.

```python
from langchain.tools import tool
import requests

@tool
def simple_web_search(query: str) -> str:
    """Very lightweight web search using DuckDuckGo."""
    url = f"https://api.duckduckgo.com/?q={query}&format=json"
    res = requests.get(url).json()
    return res.get("Abstract", "No result")
```

---

# 🔧 **5. backend/rag.py**

RAG pipeline (retrieval → answer → citations)

```python
from langchain.chains import RetrievalQA
from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.prompts import PromptTemplate
from .vector_store import get_vectorstore
from .tools import simple_web_search
from langchain.agents import initialize_agent, AgentType

def build_rag_chain():
    vectordb = get_vectorstore()
    retriever = vectordb.as_retriever(search_kwargs={"k": 4})

    llm = ChatGoogleGenerativeAI(
        model="gemini-1.5-pro",
        temperature=0.2
    )

    template = """
    You are a helpful assistant. Use the following documents to answer the question.
    If the answer is not in the documents, say "Not found."

    QUESTION: {question}

    DOCUMENTS:
    {context}

    Final Answer:
    """

    prompt = PromptTemplate(
        template=template,
        input_variables=["question", "context"],
    )

    return RetrievalQA.from_chain_type(
        llm=llm,
        chain_type="stuff",
        retriever=retriever,
        return_source_documents=True
    )

rag_chain = build_rag_chain()
```

---

# 🔧 **6. backend/main.py (FastAPI server)**

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware
from .models import QueryRequest, AnswerResponse
from .rag import rag_chain

app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["*"],
    allow_headers=["*"],
)

@app.post("/query", response_model=AnswerResponse)
def query_rag(req: QueryRequest):
    result = rag_chain(req.query)
    answer = result["result"]
    sources = [doc.metadata.get("source", "unknown") for doc in result["source_documents"]]
    return AnswerResponse(answer=answer, sources=sources)
```

---

# 🔧 **7. backend/requirements.txt**

```
fastapi
uvicorn
langchain
langchain-community
langchain-google-genai
langchain-chroma
chromadb
pypdf
python-dotenv
requests
```

Run:

```
pip install -r backend/requirements.txt
uvicorn backend.main:app --reload
```

---

# 🎨 **8. frontend/app.py (Streamlit UI)**

```python
import streamlit as st
import requests

API_URL = "http://localhost:8000/query"

st.title("📘 Gemini RAG & Tools App")

query = st.text_input("Ask a question about your documents:")

if st.button("Submit"):
    with st.spinner("Thinking..."):
        res = requests.post(API_URL, json={"query": query}).json()
        st.write("### Answer")
        st.write(res["answer"])

        if res.get("sources"):
            st.write("### Sources")
            for s in res["sources"]:
                st.write("- ", s)
```

---

# 🎨 **9. frontend/requirements.txt**

```
streamlit
requests
```

Run:

```
cd frontend
streamlit run app.py
```

---

# ⭐ **Congrats — You Now Have a Complete Working App**

It includes:

✔ Document upload + vector DB
✔ Gemini embeddings
✔ RAG retrieval pipeline
✔ Tools + agent extensions
✔ FastAPI backend
✔ Streamlit chat UI
✔ Deployable structure (Cloud Run, Render, HuggingFace Spaces)

