# **Post-Course Quiz — Gemini API + LangChain**

**Total Points:** 25

---

## **1. Multiple Choice (1 point each)**

1. Which of the following is the main purpose of **retrieval-augmented generation (RAG)**?
   a) To train a new LLM from scratch
   b) To retrieve relevant documents and combine them with AI-generated responses ✅
   c) To deploy AI applications to the cloud
   d) To generate HTML templates

**Answer:** b

2. Which folder in a Flask app stores HTML templates?
   a) static
   b) templates ✅
   c) frontend
   d) backend

**Answer:** b

3. Which LangChain component allows reasoning over documents and executing tools?
   a) Embeddings
   b) RAG Chain
   c) Agent ✅
   d) Vector store

**Answer:** c

4. Which of these is **NOT** a benefit of using Gemini API?
   a) Access to advanced LLM capabilities
   b) Ability to execute multi-step reasoning ✅
   c) Provides a user interface for HTML templates ✅
   d) Supports tool integration

**Answer:** c

5. What is the main purpose of **vector embeddings**?
   a) Represent text as numerical vectors for semantic similarity ✅
   b) Store web pages for frontend rendering
   c) Execute Python code in the browser
   d) Format LLM output

**Answer:** a

**Subtotal:** 5 points

---

## **2. True / False (1 point each)**

6. Agents in LangChain can call multiple tools and reason over retrieved documents. ✅ True

7. Frontend code handles all AI reasoning and document retrieval. ❌ False

8. Persisting a vector store allows you to reuse embeddings across sessions. ✅ True

**Subtotal:** 3 points

---

## **3. Short Answer (2 points each)**

9. Describe the **flow of a user query** from frontend to final AI response in your application.

**Answer:**
User submits query → Frontend sends query to backend → Agent uses RAG + Tools → Generates response → Response returned to frontend → Displayed to user ✅

10. Give two examples of **tools** you integrated or could integrate into your agent.

**Answer Examples:**

* Calculator ✅
* Web API fetch ✅
* Date/time converter ✅
* Unit converter ✅

11. Name one **benefit of using RAG with Gemini API** in AI applications.

**Answer Examples:**

* Provides accurate, context-aware responses ✅
* Reduces hallucination in AI output ✅
* Allows multi-step reasoning using document context ✅

**Subtotal:** 6 points

---

## **4. Practical / Coding (3 points each)**

12. You want your agent to perform a calculation and explain a concept. Write a **pseudo-Python snippet** showing how you would run the agent.

**Sample Answer:**

```python
query = "Explain embeddings and calculate 12*12"
response = agent.run(query)
print(response)
```

✅ Accept equivalent code snippets.

13. How do you **persist and reload** a FAISS vector store for reuse?

**Sample Answer:**

```python
vectorstore.save_local("persist_dir")    # Persist
vectorstore = FAISS.load_local("persist_dir", embeddings)   # Reload
```

✅ Accept equivalent correct commands.

**Subtotal:** 6 points

---

## **5. Discussion / Conceptual (2 points)**

14. Explain **why combining Gemini API with LangChain** is effective for building AI applications.

**Sample Answer:**

* Gemini API provides powerful LLMs for reasoning and text generation ✅
* LangChain provides structure (agents, chains, tools) for multi-step workflows ✅
* Together, they enable AI applications to perform document retrieval, tool execution, and context-aware responses efficiently ✅

**Points:** Up to 2 points for completeness

---

## **6. Optional Bonus (2 points)**

15. Suggest one **real-world application** you could build using the full stack of Gemini API + LangChain + Frontend.

**Sample Answers:**

* AI-powered research assistant ✅
* Customer support chatbot ✅
* Knowledge management tool ✅
* Document summarization and Q&A system ✅

**Points:** 2 points

---

# **Grading Summary**

| Section            | Points                    |
| ------------------ | ------------------------- |
| Multiple Choice    | 5                         |
| True / False       | 3                         |
| Short Answer       | 6                         |
| Practical / Coding | 6                         |
| Discussion         | 2                         |
| Bonus              | 2                         |
| **Total**          | 24–26 points (with bonus) |

---

# **Answer Key (Quick Reference)**

**MCQs:** 1-b, 2-b, 3-c, 4-c, 5-a
**True/False:** 6-T, 7-F, 8-T
**Short Answer:** 9-query flow, 10-tools, 11-RAG benefit
**Practical:** 12-agent.run(), 13-save/load vector store
**Discussion:** Gemini API + LangChain synergy for reasoning + tool execution
**Bonus:** Any valid real-world AI application

---

This **post-course quiz** evaluates learners’ **conceptual understanding, coding ability, and practical knowledge**, ensuring they’ve achieved the learning outcomes of the 3-day course.

---

