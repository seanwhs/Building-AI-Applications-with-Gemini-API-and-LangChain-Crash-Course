# **Day 2 Quiz — RAG, Tools & Agents**

**Total Points:** 25
**Time:** 20–30 minutes

---

## **Section A — Multiple Choice (1 point each)**

1. What does RAG stand for?
   a) Retrieval and Generation
   b) Random Access Generation
   c) Recurrent AI Generation
   d) Rapid Algorithmic Guidance

2. Which component retrieves relevant document chunks in a RAG pipeline?
   a) LLM
   b) Vector store / retriever
   c) Agent
   d) Tool

3. In LangChain, what is the primary purpose of a `Tool`?
   a) Store embeddings
   b) Execute external functions or API calls
   c) Chunk documents
   d) Generate embeddings

4. What does the `verbose=True` parameter do when initializing an agent?
   a) Limits the output
   b) Shows step-by-step reasoning of the agent
   c) Automatically calls all tools
   d) Generates random text

5. Which chain type is commonly used for simple RAG pipelines?
   a) `map_reduce`
   b) `stuff`
   c) `refine`
   d) `react`

---

## **Section B — Short Answer (2 points each)**

6. Explain why returning source documents in RAG is important.

7. What are the benefits of using agents with tools compared to only using an LLM?

8. Describe one scenario where a custom tool might be necessary in an AI assistant.

---

## **Section C — Practical / Coding (3 points each)**

9. **Vector Store Query**
   Write a Python snippet to load a persisted Chroma vector store and retrieve the top 3 documents for the query `"Explain embeddings"`.

10. **Tool Creation**
    Write a Python function and `Tool` object in LangChain that calculates the square of a given number.

11. **Agent Execution**
    Show how to initialize an agent with the tool from question 10 and run a query to calculate the square of 12.

---

## **Section D — True/False (1 point each)**

12. Agents in LangChain can autonomously decide which tool to use based on the query. (T/F)

13. RAG pipelines require fine-tuning the LLM to function properly. (T/F)

14. It is safe to use Python’s `eval()` on untrusted user input in a production tool. (T/F)

---

### **Answer Key (Suggested)**

**Multiple Choice:**
1-a, 2-b, 3-b, 4-b, 5-b

**Short Answer:**
6. For transparency, to validate responses, and allow users to trace back the answer to the source documents.
7. Agents allow multi-step reasoning, can use external tools/APIs, and perform tasks beyond text generation.
8. Example: Calculating complex arithmetic, performing a web search, or querying an external database.

**Practical / Coding:**

9.

```python
from vector_store import get_vectordb

vectordb = get_vectordb(persist_dir="./chroma_db")
results = vectordb.similarity_search("Explain embeddings", k=3)
for doc in results:
    print(doc.page_content[:200])
```

10.

```python
from langchain.agents import Tool

def square_fn(n: int) -> int:
    return n * n

square_tool = Tool(
    name="SquareCalculator",
    func=square_fn,
    description="Calculates the square of a number"
)
```

11.

```python
from langchain.agents import initialize_agent, AgentType
from langchain_google_genai import ChatGoogleGenerativeAI

llm = ChatGoogleGenerativeAI(model="gemini-1.5-pro")
tools = [square_tool]

agent = initialize_agent(tools=tools, llm=llm, agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION, verbose=True)
agent.run("Calculate the square of 12")
```

**True/False:**
12-T, 13-F, 14-F

---

This quiz reinforces **conceptual understanding, practical skills, and coding competence** from Day 2.
