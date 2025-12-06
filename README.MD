# 🚀 **3-Day Course Syllabus**

## **“Building AI Applications with Gemini API and LangChain – Crash Course”**

**Format:** Hands-on, project-driven
**Outcome:** Each student builds & deploys a complete AI application by Day 3

---

# **📅 Day 1 — Foundations + Core LLM Workflows**

## **Module 1 — Introduction, Setup & Architecture (45 min)**

**Topics**

* Gemini models overview
* LangChain fundamentals (LCEL, Chains, Runnables)
* Planning the full application you’ll build (RAG + tools + UI)
* Environment setup (Python, APIs, LangChain, vector DB)

**Hands-On**

* “Hello Gemini” in LangChain
* Set up the project workspace + GitHub repo

---

## **Module 2 — Prompting, Chains, and Structured Output (90 min)**

**Topics**

* PromptTemplates
* LLMChain + LCEL basics
* JSON structured outputs
* Pydantic parsing & robust outputs

**Hands-On**

* Build reusable prompt + chain components
* Implement structured output mini-tools
* **Integrate these into your final project scaffolding**

---

## **Module 3 — Embeddings, Vector Stores & Document Loading (120 min)**

**Topics**

* Gemini embeddings
* Vector stores (FAISS / Chroma)
* Document loaders (PDFs, web pages, text files)
* Indexing + chunking strategies

**Hands-On**

* Load sample documents for your capstone app
* Create embeddings + build vector store
* Test vector search queries

**🎯 Day 1 Project Milestone:**
Your app can **load documents + embed them + run similarity search**.

---

---

# **📅 Day 2 — RAG + Agents + Tools**

## **Module 4 — Building a Full RAG Pipeline (2 hours)**

**Topics**

* RAG architecture
* Retriever configuration
* Context compression
* Answers with citations
* Query rewriting (optional advanced)

**Hands-On**

* Implement full RAG chain using LCEL
* Add context compression
* Add citations and evaluation tests

**Integrated Into Project:**
Your app becomes a **document-aware question-answering assistant**.

---

## **Module 5 — Tools, Function Calling & Agents (90 min)**

**Topics**

* Gemini function calling
* LangChain tools
* Agents vs. Chains
* Safety, determinism & tool orchestration

**Hands-On**

* Build tools (search, calculator, scraper, etc.)
* Add them to your RAG app as agent tools
* Create an agent that combines RAG + tools

**Project Integration:**
Your app now can **use tools and functions to enhance answers**.

---

## **Module 6 — Intro to Multimodal Gemini (60 min)**

**Topics**

* Gemini Vision model
* Image input processing in LangChain
* OCR & image QA

**Hands-On**

* Add optional image understanding to your project
  (Example: “upload invoice → answer questions”, “upload screenshot → explain”)

**🎯 Day 2 Project Milestone:**
Your app is now a **tool-using, multimodal-ready RAG assistant**.

---

---

# **📅 Day 3 — UI, Deployment & Capstone Application**

## **Module 7 — Building a Front-End UI (90 min)**

**Choose a stack:**

* **Streamlit** (recommended quick build)
* or **Gradio**
* or **Simple FastAPI REST endpoint**

**Topics**

* Creating a clean chat interface
* Image upload fields
* Displaying model responses, citations, and debug traces

**Hands-On**

* Build your app’s front-end
* Connect front-end ↔ backend chains

---

## **Module 8 — Deployment & Productionizing (90 min)**

**Topics**

* Deploying to cloud (HuggingFace Spaces / Render / Google Cloud Run)
* Caching & rate-limit handling
* Logging, validation & monitoring
* Managing secrets

**Hands-On**

* Deploy your app to a hosting platform
* Add input/output validation
* Add basic logging & chain tracing

---

## **Module 9 — Capstone Finalization & Demo (2–3 hours)**

**Tasks**

* Polish UI
* Refine RAG
* Add optional advanced features:

  * Memory
  * Query rewriting
  * Multi-document support
  * Tool-enhanced reasoning
* Prepare a mini demo

**Final Deliverables:**

* **Fully working AI application**
* **Hosted online** (URL provided)
* **GitHub repository with code**
* **Short demo presentation**

---

# ⭐ Final Application Example (What Students Will Build)

A complete **AI Knowledge Assistant** with:

* Document upload
* Automated chunking + embeddings
* RAG query answering with citations
* Optional image understanding
* Tool-using agent capabilities
* User-friendly web UI
* Cloud deployment

