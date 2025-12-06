# 📘 **TRAINER GUIDE**

## *Building AI Applications with Gemini API & LangChain – 3-Day Crash Course*

---

# 🎯 **Course Goal**

By the end of this course, learners will be able to build a fully functional **AI Knowledge Assistant** using:

* Gemini API (LLM + embeddings + vision)
* LangChain (chains, retrieval, tools, agents)
* Chroma (vector database)
* FastAPI & Streamlit (backend + frontend)

Learners will complete a **capstone project** deployable in the cloud.

---

# 🗂️ **Trainer Objectives**

* Explain complex AI/LLM concepts in simple language
* Conduct live coding demos
* Guide learners through hands-on labs
* Troubleshoot common issues
* Encourage experimentation and confidence
* Assess learner milestones

---

# 🕒 **Course Schedule (High Level)**

| Day | Focus                           | Trainer Tasks                            | Lab Focus                                        | Milestone                   |
| --- | ------------------------------- | ---------------------------------------- | ------------------------------------------------ | --------------------------- |
| 1   | Foundations + Document Pipeline | Slides, demo, environment setup          | Document loading, chunking, embedding, vector DB | Functional vector retrieval |
| 2   | RAG + Tools + Agents            | Explain chains, agents, tool integration | Build RAG chain, add tools, optional vision      | RAG backend ready           |
| 3   | UI + Deployment + Capstone      | Frontend + API, deployment strategies    | Build Streamlit UI, deploy, present              | Final deployable app        |

---

# --------------------------------------------------

# **DAY 1 — Trainer Guide**

### *Foundations + Document Pipeline*

**Duration:** 4–5 hours (lecture + demo + lab)

---

## **1. Welcome & Orientation (15 min)**

**Trainer Tips:**

* Show the capstone demo first to inspire learners
* Emphasize that no prior AI experience is needed
* Explain 3-day roadmap

**Slides:** 1–4
**Activities:** Q&A

---

## **2. Gemini + LangChain Architecture (20 min)**

**Trainer Tips:**

* Show simple and detailed architecture diagrams
* Explain embeddings, retrieval, and RAG pipeline
* Use analogies like “LLM = brain, vector store = memory”

**Slides:** 5–8
**Demo:** Point out code modules and their roles

---

## **3. Environment Setup (25 min)**

**Trainer Tips:**

* Guide learners through `pip install` and `.env` configuration
* Validate Gemini key via live demo
* Ensure learners can print a model object

**Slides:** 9–10
**Lab Part 1:** Environment validation

---

## **4. Document Loading (30 min)**

**Trainer Tips:**

* Show PyPDFLoader and TextLoader usage
* Explain metadata handling
* Encourage learners to explore their own PDFs

**Slides:** 11
**Lab Part 2:** Load documents and inspect `Document` objects

---

## **5. Chunking (35 min)**

**Trainer Tips:**

* Explain chunk_size and overlap
* Visualize how a long PDF is split
* Show effect on token limits

**Slides:** 12–13
**Lab Part 3:** Chunk documents, experiment with sizes

---

## **6. Embeddings with Gemini (30 min)**

**Trainer Tips:**

* Explain concept of vector embeddings
* Demonstrate embedding a sentence or paragraph
* Show semantic similarity examples

**Slides:** 14–15
**Lab Part 4:** Embed sample sentences, compare results

---

## **7. Vector Store with Chroma (35 min)**

**Trainer Tips:**

* Walk through `vector_store.py` code
* Demonstrate building DB, persisting it
* Show similarity search and explain results

**Slides:** 16–18
**Lab Part 5 & 6:** Build DB, retrieve top results

---

## **8. Day 1 Lab & Milestone (90–120 min)**

**Trainer Role:**

* Supervise hands-on lab completion
* Encourage learners to troubleshoot errors
* Confirm vector DB is working
* Optional: stretch challenges (FAISS, metadata)

**Milestone:** Learners can load docs → embed → query vector DB successfully

---

## **9. Wrap-Up & Homework (10 min)**

**Trainer Tips:**

* Recap Day 1 objectives
* Highlight what is coming Day 2
* Optional homework: add more documents, tweak chunk size, try embedding alternatives

---

# --------------------------------------------------

# **DAY 2 & DAY 3 OVERVIEW**

**Day 2:** RAG + Tools + Agents

* Explain RetrievalQA, chains, tools
* Demonstrate adding custom tool functions
* Show agent initialization
* Lab: build RAG chain + tools

**Day 3:** UI + Deployment + Capstone

* Explain FastAPI + Streamlit integration
* Demonstrate deployment (Render/HuggingFace)
* Lab: connect UI to backend, deploy, demo
* Capstone: students present apps

---

# --------------------------------------------------

# **Trainer Tips for Success**

* **Live Code**: Always demo first, then learners replicate
* **Pacing**: Pause frequently for questions
* **Debugging**: Prepare common errors in advance
* **Encouragement**: Remind learners mistakes are normal
* **Optional Stretch**: Vision multimodal, FAISS vector store, LangGraph

---

# --------------------------------------------------

# **Assessment & Milestones**

| Milestone | Assessment                          |
| --------- | ----------------------------------- |
| Day 1     | Vector DB is built & searchable     |
| Day 2     | RAG backend + tools functional      |
| Day 3     | Full UI + deployment + working demo |

Trainer observes lab completion and gives feedback.

---

# --------------------------------------------------

# **Resources for Trainer**

* Slides (Day 1–3)
* Lab Instructions (Day 1–3)
* Sample Documents
* Example GitHub repo
* Instructor Notes / Troubleshooting Checklist

---

# ✅ **Optional Enhancements**

* Record demo videos for students
* Create a “common errors” slide deck
* Provide extra exercises: multimodal, FAISS, metadata

