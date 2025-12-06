# **Day 2 Notes — RAG, Tools & Agents**

### *Gemini API + LangChain Crash Course*

---

## **1. Introduction**

**Focus:** Build an intelligent AI backend capable of:

* **RAG (Retrieval-Augmented Generation)** — query documents with context
* **Tools** — extend AI functionality with external operations
* **Agents** — multi-step reasoning combining LLM + tools

**Prerequisites:** Completion of Day 1 — vector store, embeddings, document chunking

**Goal:** By the end of Day 2, learners can build a RAG-based assistant, integrate tools, and run agents.

---

## **2. Recap — Day 1 Key Concepts**

* **Document Loading:** PDFs, TXT, CSV → LangChain `Document` objects
* **Chunking:** `RecursiveCharacterTextSplitter` → manageable chunks with overlap
* **Embeddings:** Gemini API generates vector representations of text
* **Vector Store:** Chroma stores embeddings for semantic search

**Key Takeaway:** Vector store enables **context-aware retrieval**, which is foundational for RAG.

---

## **3. Retrieval-Augmented Generation (RAG)**

### **3.1 Concept**

RAG combines **retrieval** (vector store) and **generation** (LLM) to answer questions over large datasets.

**Steps:**

1. User query → Retriever finds top `k` relevant chunks
2. Chunks are fed into LLM (Gemini)
3. LLM generates answer using retrieved context

**Advantages:**

* Accurate answers over large corpora
* Scales without LLM fine-tuning
* Transparency via returned source documents

**Visual Representation:**

```
User Query
    ↓
Retriever (Vector Store)
    ↓
Relevant Chunks
    ↓
LLM (Gemini)
    ↓
Answer + Source Documents
```

---

### **3.2 Implementation Steps**

**1. Load Vector Store:**

```python
from vector_store import get_vectordb
vectordb = get_vectordb(persist_dir="./chroma_db")
```

**2. Create Retriever:**

```python
retriever = vectordb.as_retriever(search_type="similarity", search_kwargs={"k":3})
```

**3. Initialize Gemini LLM:**

```python
from langchain_google_genai import ChatGoogleGenerativeAI
llm = ChatGoogleGenerativeAI(model="gemini-1.5-pro")
```

**4. Build RAG Chain:**

```python
from langchain.chains import RetrievalQA
rag_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff",
    retriever=retriever,
    return_source_documents=True
)
```

**5. Test Query:**

```python
result = rag_chain("What is the purpose of embeddings?")
print(result['result'])
print([doc.metadata for doc in result['source_documents']])
```

**Tip:** Always inspect **source documents** for context accuracy.

---

## **4. Tools**

### **4.1 Concept**

* Tools **extend LLM capabilities**
* Examples: Calculator, web search, translation, API calls

**Benefits:**

* Automate tasks LLM cannot perform directly
* Enable real-world functionality

### **4.2 Creating a Custom Tool**

```python
from langchain.agents import Tool

def calculator_fn(query: str) -> str:
    try:
        return str(eval(query))  # Caution: unsafe for untrusted input
    except Exception:
        return "Invalid calculation"

calculator_tool = Tool(
    name="Calculator",
    func=calculator_fn,
    description="Performs basic arithmetic operations"
)
```

**Best Practices:**

* Keep tools modular
* Name tools descriptively
* Validate inputs to avoid unsafe execution

---

## **5. Agents**

### **5.1 Concept**

* Agents = LLM + Tools + Reasoning
* Can **autonomously decide** which tool to use
* Enable **multi-step reasoning**

**LangChain Agent Types:**

* `ZERO_SHOT_REACT_DESCRIPTION` — chooses tools based on descriptions
* `SELF_ASK_WITH_SEARCH` — can chain multiple queries

**Steps:**

1. Receive query
2. Determine appropriate tool
3. Execute tool
4. Generate final answer

**Visual Representation:**

```
User Query
    ↓
Agent
    ↓           ↘
   Tool(s)       LLM
      ↓           ↓
   Tool Output → Combine → Final Answer
```

---

### **5.2 Initializing an Agent**

```python
from langchain.agents import initialize_agent, AgentType

tools = [calculator_tool]

agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION,
    verbose=True
)
```

### **5.3 Running Agent Queries**

```python
agent.run("Calculate 23 * 19 and summarize the result in one sentence.")
```

**Expected Outcome:**

* Agent executes calculation
* Provides reasoning steps
* Generates final answer

**Tip:** Use `verbose=True` to show step-by-step reasoning.

---

## **6. Combining RAG + Agents**

* **Scenario:** User query requires both document retrieval and a tool calculation
* **Approach:** Pass retrieved document context to agent along with tool access
* **Benefit:** Produces **contextually accurate answers** while performing computations

---

## **7. Advanced Concepts**

* **Multiple Tools:** Add more tools for extended AI functionality
* **Chain Types:** `stuff`, `map_reduce`, `refine` — useful for long contexts
* **Source Tracking:** Always include document metadata for transparency
* **Error Handling:** Ensure robust input validation in tools

---

## **8. Lab Exercises Checklist**

1. Load persisted vector store
2. Build RAG chain & run test queries
3. Create a calculator tool
4. Initialize an agent & run multi-step queries
5. Optional: Integrate additional tools

---

## **9. Common Errors & Troubleshooting**

| Issue                          | Solution                                          |
| ------------------------------ | ------------------------------------------------- |
| RAG returns irrelevant results | Increase `k`, check chunk size & overlap          |
| Agent fails to call tool       | Verify tool initialization and registration       |
| ModuleNotFoundError            | Run `pip install -r requirements.txt`             |
| Unsafe calculation errors      | Avoid `eval` on untrusted input; validate queries |

---

## **10. Key Takeaways**

* **RAG** allows context-aware AI responses from large documents
* **Tools** extend AI capabilities beyond text generation
* **Agents** enable multi-step reasoning and tool execution
* Combining RAG + Agents creates a **powerful AI backend**
* Day 2 prepares for **frontend integration on Day 3**

---

These detailed notes provide learners with **conceptual understanding, practical coding examples, and tips for real-world application**.

---
