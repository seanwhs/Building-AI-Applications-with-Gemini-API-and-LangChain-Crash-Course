# 📘 **Day 2 — README**

## *Building AI Applications with Gemini API & LangChain*

### **Focus:** Retrieval-Augmented Generation (RAG), Tools, and Agents

---

## **Course Objective — Day 2**

Today, you will take the foundation from **Day 1** and:

1. Build a **Retrieval-Augmented Generation (RAG) pipeline**
2. Integrate **tools and function calls** to extend the assistant’s capabilities
3. Create and test **LangChain Agents** for multi-step reasoning

By the end of the day, your backend AI assistant will be able to:

* Answer questions over uploaded documents
* Cite sources for responses
* Use tools to perform computations or API queries
* Execute multi-step reasoning through agents

---

## **Pre-requisites**

* Completion of **Day 1 labs**: Document loading, chunking, embeddings, vector store creation
* Python 3.10+ environment
* Gemini API key set in `.env`
* Vector store built and persisted (`./chroma_db`)

---

## **Folder Structure (Day 2)**

```
backend/
├── config.py         # API keys, constants
├── vector_store.py   # Chroma vector store
├── rag.py            # Retrieval + LLM pipeline
├── tools.py          # Custom tools for the AI
├── agents.py         # LangChain agents
├── main.py           # FastAPI backend entry point
└── requirements.txt
```

---

## **Step 1 — Loading the Vector Store**

Re-use your Day 1 vector store:

```python
from vector_store import get_vectordb

vectordb = get_vectordb(persist_dir="./chroma_db")
```

* `get_vectordb()` should load your persisted Chroma DB
* Verify retrieval works:

```python
results = vectordb.similarity_search("Explain AI document processing")
print(results[0].page_content[:400])
```

---

## **Step 2 — Building a RAG Chain**

1. Import Gemini LLM:

```python
from langchain_google_genai import ChatGoogleGenerativeAI

llm = ChatGoogleGenerativeAI(model="gemini-1.5-pro")
```

2. Create a **RetrievalQA chain**:

```python
from langchain.chains import RetrievalQA

retriever = vectordb.as_retriever(search_type="similarity", search_kwargs={"k":3})

rag_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff",
    retriever=retriever,
    return_source_documents=True
)
```

3. Test the chain:

```python
query = "What is the main purpose of embeddings?"
result = rag_chain(query)
print(result['result'])
```

* Should return **context-aware answer** with source documents

---

## **Step 3 — Adding Tools**

* Tools extend the assistant beyond document retrieval
* Examples:

  * Calculator
  * Web search API
  * Custom function call

**Example Tool — Calculator:**

```python
from langchain.agents import Tool

def calculator_fn(query: str) -> str:
    try:
        return str(eval(query))
    except:
        return "Error in calculation."

calculator_tool = Tool(
    name="Calculator",
    func=calculator_fn,
    description="Performs basic arithmetic operations"
)
```

---

## **Step 4 — Creating a LangChain Agent**

* Agents allow **multi-step reasoning** and tool usage
* Initialize an **LLM agent** with your tools:

```python
from langchain.agents import initialize_agent
from langchain.agents import AgentType

tools = [calculator_tool]  # add more tools as needed

agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION,
    verbose=True
)
```

* Test agent with queries:

```python
agent.run("Calculate 23*19 and summarize the result in one sentence.")
```

* Output should show **step-by-step reasoning** using the tool

---

## **Step 5 — Optional: Multimodal (Vision) Gemini**

* Gemini supports **image-based queries**
* Example:

```python
from langchain.prompts import PromptTemplate

image_query = "Describe this image in detail."
```

* Advanced: Integrate an **image loader** with RAG or agent

---

## **Step 6 — Testing & Milestone Check**

By the end of Day 2, learners should have:

* RAG chain answering questions with **source documents**
* At least one **custom tool integrated**
* LangChain **agent capable of reasoning and tool execution**

**Optional Stretch:**

* Add multiple tools (search, weather, translation)
* Experiment with different chain types (`map_reduce`, `refine`)

---

## **Step 7 — Suggested Lab Exercises**

| Lab | Task                                 | Outcome                                 |
| --- | ------------------------------------ | --------------------------------------- |
| 1   | Load persisted vector store          | Confirm retrieval works                 |
| 2   | Build RAG chain with Gemini          | AI answers queries contextually         |
| 3   | Create a calculator tool             | Tool returns arithmetic results         |
| 4   | Initialize LangChain agent           | Agent can use tool + LLM reasoning      |
| 5   | (Optional) Integrate image query     | Multimodal capabilities                 |
| 6   | Experiment with multiple chain types | Compare `stuff`, `map_reduce`, `refine` |

---

## **Notes & Best Practices**

* Always return **source documents** with answers for transparency
* Use **overlap** from Day 1 chunking to avoid losing context
* Modularize tools for **extensibility**
* Agents are powerful — test carefully to avoid **unintended tool execution**

---

## **References**

* [LangChain Documentation](https://docs.langchain.com/)
* [Gemini API Overview](https://ai.google/learn)
* [Chroma Vector Database](https://www.trychroma.com/)

---

✅ **Day 2 Outcome:**
You now have a **fully functional AI backend** capable of **RAG, tool execution, and agent reasoning**, ready for **frontend integration** on Day 3.

