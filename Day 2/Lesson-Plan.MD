# **Day 2 Lesson Plan — RAG, Tools & Agents**

### *Gemini API + LangChain Crash Course*

---

## **Lesson Overview**

**Theme:** Building intelligent AI with Retrieval-Augmented Generation (RAG), Tools, and Agents
**Duration:** 4–5 hours
**Mode:** Instructor-led, live coding demos, hands-on labs
**Prerequisites:** Completion of Day 1 labs (vector store, embeddings, document chunking)

**Learning Outcomes:**
By the end of Day 2, learners will be able to:

1. Explain the concept of RAG and its advantages
2. Build a RAG pipeline using Gemini API and LangChain
3. Create and integrate custom tools into AI workflows
4. Initialize and test LangChain agents for multi-step reasoning
5. Debug common errors related to RAG, tools, and agents

---

## **Lesson Schedule**

| Time      | Topic                | Activity                                                                                       | Learning Outcome                                          | Materials                     |
| --------- | -------------------- | ---------------------------------------------------------------------------------------------- | --------------------------------------------------------- | ----------------------------- |
| 0:00–0:15 | Welcome & Recap      | Discuss Day 1: document loading, chunking, embeddings, vector store                            | Recall Day 1 foundation for RAG                           | Slides                        |
| 0:15–0:45 | Introduction to RAG  | Lecture + diagram                                                                              | Understand retrieval + generation pipeline                | Slides, diagrams              |
| 0:45–1:30 | Building a RAG Chain | Live coding demo: load vector store, create retriever, initialize LLM, build RetrievalQA chain | Learners build a functional RAG pipeline                  | Code editor, README           |
| 1:30–2:15 | Custom Tools         | Lecture + demo: create calculator tool                                                         | Understand purpose and implementation of tools            | Code editor, slides           |
| 2:15–3:00 | Agents               | Lecture + live demo: initialize agent, run queries with tools                                  | Learners can combine LLM + tools for reasoning            | Code editor, slides           |
| 3:00–3:15 | Break                | Q&A, discuss challenges                                                                        | Clarify doubts and prepare for lab                        | —                             |
| 3:15–4:00 | Lab Exercises        | Hands-on: RAG queries, tool creation, agent queries                                            | Apply concepts independently and reinforce learning       | Lab instructions, code editor |
| 4:00–4:30 | Advanced Concepts    | Lecture + discussion: multi-tool agents, chain types, verbose debugging                        | Extend RAG and agent capabilities                         | Slides                        |
| 4:30–4:45 | Wrap-up & Reflection | Recap milestones, Q&A, prep for Day 3                                                          | Consolidate learning and prepare for frontend integration | Slides                        |

---

## **Instructional Strategies**

* **Direct Instruction:** Explain concepts of RAG, tools, and agents
* **Live Coding:** Demonstrate key workflows (RAG chain, tool, agent)
* **Guided Practice:** Learners follow along in real time
* **Independent Practice:** Hands-on lab exercises
* **Discussion & Reflection:** Encourage questions and real-world application discussions

---

## **Assessment & Evaluation**

* **Formative Assessment:** Observe learners during live coding and lab exercises
* **Summative Assessment:** Completion and correctness of lab exercises (RAG + agent queries)
* **Checkpoints:**

  * Can learners retrieve relevant chunks from the vector store?
  * Can they create and integrate a tool successfully?
  * Can they initialize and run an agent query correctly?

---

## **Resources & Materials**

* Day 2 Slide Deck
* README & Learner Guide
* Lab instructions and sample documents
* Python 3.10+ environment
* Gemini API key in `.env`
* Code editor (VS Code, PyCharm, or Jupyter)

---

## **Milestones / Checklist**

* [ ] Vector store is functional and returns relevant chunks
* [ ] RAG chain produces accurate answers with source documents
* [ ] Custom tool is created and works correctly
* [ ] Agent executes multi-step reasoning using tools
* [ ] Learners are ready for Day 3 frontend integration

---

## **Trainer Notes**

* Encourage learners to **explain RAG in their own words**
* Highlight **verbose agent output** for reasoning transparency
* Emphasize **modular tools** and **source document tracking**
* Be prepared to troubleshoot: irrelevant RAG results, tool errors, or API issues

---

This lesson plan aligns with the **Day 2 slides, lab, learner guide, trainer guide, and quiz**, providing a **cohesive, structured approach** for Day 2.

---
