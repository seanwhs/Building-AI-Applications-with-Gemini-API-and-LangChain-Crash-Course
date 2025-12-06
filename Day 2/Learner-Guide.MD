Here’s a **comprehensive Day 2 Learner Guide** for your **Gemini API + LangChain Crash Course**. It’s designed for learners to follow along, take notes, and have a detailed reference for **RAG, Tools, and Agents**.

---

# **Day 2 Learner Guide — RAG, Tools & Agents**

### *Building AI Applications with Gemini API & LangChain*

---

## **1. Introduction**

**Objective of Day 2:**
Build on the foundation from Day 1 to create an **intelligent AI backend** capable of:

* **Retrieval-Augmented Generation (RAG)**: Answer questions using document chunks
* **Tools**: Perform external computations or API tasks
* **Agents**: Multi-step reasoning combining LLM + tools

By the end of the day, you will have a **backend AI assistant** ready for frontend integration on Day 3.

---

## **2. Recap — Day 1 Foundations**

* Documents loaded (PDFs, TXT)
* Chunked using `RecursiveCharacterTextSplitter`
* Embeddings generated using Gemini API
* Vector store (Chroma) built and persisted

**Key Takeaway:** Today we use these embeddings and vector store for **context-aware responses**.

---

## **3. Retrieval-Augmented Generation (RAG)**

### **3.1 Concept**

* Combines **retrieval** (vector store) + **generation** (LLM)
* Steps:

  1. User query → Retriever finds top `k` relevant chunks
  2. Chunks are fed to LLM (Gemini)
  3. LLM generates answer with context

**Advantages:**

* Accurate answers over large document collections
* Scalable without model fine-tuning
* Can cite source documents

### **3.2 Implementation Steps**

1. **Load vector store:**

```python
from vector_store import get_vectordb
vectordb = get_vectordb(persist_dir="./chroma_db")
```

2. **Create retriever:**

```python
retriever = vectordb.as_retriever(search_type="similarity", search_kwargs={"k":3})
```

3. **Initialize Gemini LLM:**

```python
from langchain_google_genai import ChatGoogleGenerativeAI
llm = ChatGoogleGenerativeAI(model="gemini-1.5-pro")
```

4. **Build RAG chain:**

```python
from langchain.chains import RetrievalQA
rag_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff",
    retriever=retriever,
    return_source_documents=True
)
```

5. **Test a query:**

```python
result = rag_chain("What is the purpose of embeddings?")
print(result['result'])
print([doc.metadata for doc in result['source_documents']])
```

**Tip:** Always inspect returned source documents to verify context accuracy.

---

## **4. Tools**

### **4.1 Concept**

* Tools extend AI capabilities beyond text retrieval
* Examples: calculator, web search, translation, API queries

### **4.2 Create a Custom Tool**

```python
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

**Notes:**

* Keep tool functions safe (avoid `eval` on untrusted input in production)
* Use descriptive names and clear functionality
* Modularize tools for easy extension

---

## **5. Agents**

### **5.1 Concept**

* Agents = LLM + Tools + Reasoning
* Can **autonomously decide** which tool to use
* Enable **multi-step reasoning**

### **5.2 Initialize Agent**

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

### **5.3 Test Agent**

```python
agent.run("Calculate 23*19 and summarize the result in one sentence.")
```

**Expected Outcome:**

* Agent executes calculation using tool
* Provides reasoning steps and final answer

**Tip:** `verbose=True` shows step-by-step reasoning for debugging and learning.

---

## **6. Advanced Concepts**

* **RAG + Agents:** Combine retrieval and tools for powerful AI responses
* **Multiple tools:** Add additional APIs, e.g., web search, weather, translation
* **Chain types:** Experiment with `stuff`, `map_reduce`, `refine` for long context
* **Source tracking:** Always return document metadata to increase transparency

---

## **7. Lab Exercises Checklist**

| Lab Task                    | Notes                                     |
| --------------------------- | ----------------------------------------- |
| Load persisted vector store | Verify similarity search works            |
| Build RAG chain             | Confirm answer + source documents         |
| Run test query              | Inspect output for accuracy               |
| Create calculator tool      | Ensure function works independently       |
| Initialize agent            | Agent should use tool correctly           |
| Run multi-step agent query  | Observe reasoning steps in verbose output |
| Optional: Add more tools    | Experiment with chaining multiple tools   |

---

## **8. Tips & Best Practices**

* Return **source documents** for transparency and validation
* Use **chunk overlap** from Day 1 to avoid losing context
* Keep **tools modular** for easy integration and testing
* Test agents thoroughly to prevent unintended behavior
* Use `k` in retriever to control number of chunks retrieved
* Experiment with chain types to handle large or complex queries

---

## **9. Common Issues & Troubleshooting**

| Issue                          | Solution                                                                           |
| ------------------------------ | ---------------------------------------------------------------------------------- |
| RAG returns irrelevant answers | Increase `k`, check chunk overlap and embeddings                                   |
| Agent fails to call tool       | Check that `Tool` object is correctly initialized and passed to `initialize_agent` |
| ModuleNotFoundError            | Ensure `pip install -r requirements.txt` was run                                   |
| Calculation errors             | Validate input query for proper syntax                                             |

---

## **10. Milestones for Day 2**

By the end of Day 2, you should be able to:

1. Retrieve relevant chunks from vector store
2. Use RAG chain to answer questions with sources
3. Create and integrate a custom tool
4. Initialize an agent capable of multi-step reasoning
5. Prepare backend for **frontend integration on Day 3**

---

This learner guide complements the **README**, **Lab**, and **Slides**, providing a **complete reference** for Day 2.

