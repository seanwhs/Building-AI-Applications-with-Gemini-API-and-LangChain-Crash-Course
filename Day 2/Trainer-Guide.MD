# **Day 2 Trainer Guide — RAG, Tools & Agents**

### *Building AI Applications with Gemini API & LangChain*

---

## **Session Overview**

**Duration:** 4–5 hours (can be adjusted)
**Focus:** Retrieval-Augmented Generation (RAG), Tool Integration, Agents
**Prerequisites:** Completion of Day 1 labs

**Learning Outcomes:**
By the end of Day 2, learners will be able to:

1. Build a RAG pipeline using Gemini API + LangChain
2. Integrate custom tools into AI workflows
3. Create and test agents capable of multi-step reasoning
4. Prepare backend for frontend integration

---

## **Trainer Preparation**

**Before the Session:**

* Ensure all participants have Day 1 setup completed
* Verify Python environment 3.10+
* Confirm Gemini API keys are correctly set in `.env`
* Pre-load vector store or guide learners to build it from Day 1
* Prepare demo queries for RAG and agent tests

**Required Materials:**

* Project folder: `backend/` with Day 1 files
* Sample documents (`documents/sample.pdf`)
* Lab exercise instructions
* Slide deck (Day 2)

---

## **Session Plan & Timing**

| Time      | Topic                   | Trainer Notes                                                                                                                    |
| --------- | ----------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| 0:00–0:15 | Welcome & Recap         | Review Day 1: documents, chunking, embeddings, vector store. Emphasize RAG foundation.                                           |
| 0:15–0:45 | Introduction to RAG     | Explain concept: Retrieval + Generation. Show diagram. Use a simple query demo.                                                  |
| 0:45–1:30 | Build RAG Chain         | Live coding demo: load vector store, create retriever, initialize LLM, RetrievalQA. Learners follow along.                       |
| 1:30–2:15 | Custom Tools            | Explain purpose of tools. Demonstrate creating a calculator tool. Show safe coding practices.                                    |
| 2:15–3:00 | Agents                  | Explain agent concept: multi-step reasoning, tool selection. Demo agent initialization with calculator tool. Run sample queries. |
| 3:00–3:15 | Break                   | Quick Q&A session.                                                                                                               |
| 3:15–4:00 | Lab Exercises           | Learners perform labs: RAG query, create tool, run agent. Trainer monitors, assists.                                             |
| 4:00–4:30 | Advanced Concepts & Q&A | Discuss multiple tools, chain types, source tracking, verbose debugging. Answer questions.                                       |
| 4:30–4:45 | Wrap-up                 | Recap Day 2 milestones, prepare learners for Day 3 frontend integration.                                                         |

---

## **Trainer Talking Points**

### **RAG**

* Explain why LLMs alone struggle with long documents
* Highlight importance of embeddings & vector stores
* Emphasize returning **source documents** for transparency

### **Tools**

* Demonstrate tool modularity
* Emphasize descriptive naming & clear function definitions
* Discuss safe execution of code in production

### **Agents**

* Highlight how agents **autonomously decide** which tool to use
* Show verbose output for debugging reasoning steps
* Discuss trade-offs: tool use vs LLM computation

---

## **Demo Tips**

* Use **short, clear queries** for RAG and agent demos
* Show **terminal outputs** with source documents visible
* For multi-step queries, demonstrate how agent reasoning works step-by-step
* Encourage learners to experiment with **different `k` values** and chain types

---

## **Lab Facilitation**

* Circulate among learners, helping with environment setup, API keys, or code errors
* Encourage learners to compare RAG outputs vs agent outputs
* Suggest experimenting with additional tools if time allows
* Use common errors table to anticipate troubleshooting questions

---

## **Common Errors & Solutions**

| Error                          | Trainer Guidance                                             |
| ------------------------------ | ------------------------------------------------------------ |
| RAG returns irrelevant results | Check `k` in retriever, chunk overlap, and embeddings        |
| Agent fails to call tool       | Ensure `Tool` object passed correctly to `initialize_agent`  |
| ModuleNotFoundError            | Confirm `pip install -r requirements.txt` executed           |
| Calculation errors             | Verify arithmetic string is valid, emphasize safe eval usage |

---

## **Key Milestones for Learners**

1. Vector store is functional and queries return relevant chunks
2. RAG chain can answer context-aware questions with sources
3. Custom tool is created and integrated successfully
4. Agent executes multi-step reasoning combining LLM + tool

---

## **Trainer Notes for Engagement**

* Ask learners to explain the RAG concept in their own words
* Encourage experimentation with tool integration
* Discuss real-world use cases (document Q&A, business assistants)
* Highlight best practices for modularity and scalability

---

This guide ensures trainers can **deliver Day 2 efficiently**, provide demos, support labs, and prepare learners for **Day 3 frontend integration**.

---
