
# **Day 2 Lab — RAG, Tools, and Agents**

### *Building AI Applications with Gemini API & LangChain*

---

## **Objective**

By the end of this lab, learners will be able to:

1. Load a persisted **vector store** from Day 1.
2. Build a **Retrieval-Augmented Generation (RAG) chain** using Gemini API.
3. Create a **custom tool** and integrate it with LangChain.
4. Initialize an **agent** capable of multi-step reasoning.
5. Test AI responses and tool usage.

---

## **Prerequisites**

* Completion of **Day 1**:

  * Documents loaded & chunked
  * Embeddings generated
  * Vector store persisted (`./chroma_db`)
* Python 3.10+ environment
* Gemini API key stored in `.env`

---

## **Lab Setup**

### 1. Create / Open Your Project Folder

```
backend/
├── config.py
├── vector_store.py
├── rag.py
├── tools.py
├── agents.py
└── main.py
```

---

### 2. Load Persisted Vector Store

**Objective:** Confirm that your Day 1 embeddings and chunks are retrievable.

```python
# vector_store.py
from langchain.vectorstores import Chroma
from langchain_google_genai import GoogleGenerativeAIEmbeddings

def get_vectordb(persist_dir="./chroma_db"):
    embed_model = GoogleGenerativeAIEmbeddings(model="models/embedding-001")
    vectordb = Chroma(persist_directory=persist_dir, embedding_function=embed_model)
    return vectordb

if __name__ == "__main__":
    db = get_vectordb()
    results = db.similarity_search("Explain embeddings")
    print(results[0].page_content[:400])
```

**Expected Outcome:**

* Top relevant chunk(s) printed
* Confirms vector store is functional

---

### 3. Build a RAG Chain

**Objective:** Create a chain that uses the retriever and Gemini LLM to answer queries.

```python
# rag.py
from langchain.chains import RetrievalQA
from langchain_google_genai import ChatGoogleGenerativeAI
from vector_store import get_vectordb

# Initialize LLM
llm = ChatGoogleGenerativeAI(model="gemini-1.5-pro")

# Load vector store
vectordb = get_vectordb()
retriever = vectordb.as_retriever(search_type="similarity", search_kwargs={"k":3})

# Create RetrievalQA chain
rag_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff",
    retriever=retriever,
    return_source_documents=True
)

# Test
query = "What is the purpose of document chunking?"
result = rag_chain(query)
print("Answer:", result['result'])
print("Source:", [doc.metadata for doc in result['source_documents']])
```

**Expected Outcome:**

* AI generates a context-aware answer
* Source documents are shown for transparency

---

### 4. Create a Custom Tool

**Objective:** Add a simple calculator tool to demonstrate agent functionality.

```python
# tools.py
from langchain.agents import Tool

def calculator_fn(query: str) -> str:
    try:
        return str(eval(query))
    except Exception:
        return "Invalid calculation"

calculator_tool = Tool(
    name="Calculator",
    func=calculator_fn,
    description="Performs basic arithmetic operations"
)
```

**Tip:**

* Tools can be extended to call APIs, scrape data, or perform other tasks

---

### 5. Initialize a LangChain Agent

**Objective:** Combine LLM + tools for multi-step reasoning.

```python
# agents.py
from langchain.agents import initialize_agent, AgentType
from langchain_google_genai import ChatGoogleGenerativeAI
from tools import calculator_tool

llm = ChatGoogleGenerativeAI(model="gemini-1.5-pro")
tools = [calculator_tool]

agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION,
    verbose=True
)

# Test agent
agent.run("Calculate 23*19 and summarize the result in one sentence.")
```

**Expected Outcome:**

* Agent performs calculation using the tool
* Returns step-by-step reasoning and final answer

---

### 6. Optional: Multi-tool Integration

* Add additional tools: e.g., search, date/time API, translation
* Update `tools` list and re-initialize agent
* Test multi-step queries combining retrieval + tool execution

---

## **Lab Exercises Checklist**

| Task                           | Done? |
| ------------------------------ | ----- |
| Load persisted vector store    | ☐     |
| Build RetrievalQA chain        | ☐     |
| Run query with RAG chain       | ☐     |
| Create a custom tool           | ☐     |
| Initialize agent with tool     | ☐     |
| Run multi-step agent query     | ☐     |
| Optional: Add additional tools | ☐     |

---

## **Tips & Best Practices**

* Always return **source documents** for RAG transparency
* Use `verbose=True` when testing agents to see reasoning steps
* Tools should have **descriptive names** and **clear functions**
* Modularize tools for easy extension
* If retrieval fails, ensure vector store is loaded and query is semantically relevant

---

## **Common Errors & Troubleshooting**

| Error                          | Fix                                                                                |
| ------------------------------ | ---------------------------------------------------------------------------------- |
| `ModuleNotFoundError`          | Run `pip install -r requirements.txt`                                              |
| Agent fails to call tool       | Ensure `Tool` object is correctly initialized and passed to `initialize_agent`     |
| RAG returns irrelevant results | Increase `k` in retriever search, check chunk overlap, ensure embeddings are valid |
| Calculation errors             | Ensure arithmetic string is valid Python syntax                                    |

---

## **Milestones for Day 2 Lab**

1. Vector store can retrieve relevant chunks for a query
2. RAG chain produces answers with sources
3. Custom tool can be executed by agent
4. Agent can combine LLM reasoning + tool execution

---

This lab prepares learners for **Day 3**, where they will connect the **RAG backend + agents** to a **frontend UI** and deploy the application.

---
