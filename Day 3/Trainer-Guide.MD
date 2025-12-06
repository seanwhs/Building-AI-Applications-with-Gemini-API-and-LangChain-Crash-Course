# **Day 3 Trainer Guide — Frontend Integration & Final AI Application**

### *Gemini API + LangChain Crash Course*

---

## **1. Objective**

Help learners integrate the backend (RAG + Agents + Tools) with a frontend interface to create a **fully working AI application**.

**Learning Outcomes:**
By the end of the session, learners should be able to:

1. Set up a frontend for AI queries
2. Connect frontend to the RAG + Agent backend
3. Test multi-step queries with tools and document retrieval
4. Troubleshoot common integration issues
5. Optionally extend the app with multiple tools, chat history, or UI enhancements

---

## **2. Trainer Preparation**

1. **Environment:**

   * Python 3.10+ installed
   * Gemini API key in `.env`
   * Dependencies installed (`pip install -r requirements.txt`)
   * Project structure ready (backend, frontend, documents)

2. **Materials:**

   * Day 3 Slide Deck
   * Day 3 Lab Instructions
   * Code editor (VS Code, PyCharm)
   * Browser for frontend testing

3. **Set Expectations:**

   * Learners will build a working AI application
   * Encourage experimentation with queries and tools
   * Emphasize modular design and debugging strategies

---

## **3. Lesson Flow & Trainer Notes**

| Time      | Topic                 | Trainer Guidance                                   | Notes / Tips                                                   |
| --------- | --------------------- | -------------------------------------------------- | -------------------------------------------------------------- |
| 0:00–0:15 | Welcome & Recap       | Review RAG, Tools, Agents from Days 1–2            | Ask learners to share key takeaways from Day 2                 |
| 0:15–0:45 | Frontend Overview     | Introduce Flask/Streamlit concepts and integration | Show diagram: User → Frontend → Backend → LLM/Tools → Response |
| 0:45–1:30 | Frontend Setup        | Live coding: create `app.py` and `index.html`      | Emphasize file structure and template folder placement         |
| 1:30–2:15 | Backend Integration   | Demonstrate connecting frontend to agent           | Run sample queries to show RAG + Tools in action               |
| 2:15–3:00 | Lab Session           | Guide learners through hands-on integration        | Circulate to help with errors, ensure agent.run() works        |
| 3:00–3:15 | Break                 | Answer questions, recap key points                 | Troubleshoot common issues                                     |
| 3:15–4:00 | Optional Enhancements | Demo multiple tools, chat history, UI improvements | Encourage learners to extend functionality                     |
| 4:00–4:30 | Testing & Debugging   | Demonstrate handling errors                        | Show verbose agent output, check vector store and API keys     |
| 4:30–4:45 | Wrap-up & Reflection  | Review milestones and next steps                   | Highlight deployment options and further learning paths        |

---

## **4. Demo Instructions**

1. **Frontend Form Demo:**

   * Open browser, show empty input form
   * Enter simple query: `"What is embeddings?"`

2. **Agent + RAG Demo:**

   * Run multi-step query: `"Explain embeddings and calculate 12*12"`
   * Show agent verbose reasoning
   * Highlight retrieved document context

3. **Tool Execution Demo:**

   * Run calculator or API tool
   * Show correct output and modularity

4. **Optional Enhancements Demo:**

   * Add new tool (e.g., unit converter)
   * Demonstrate chat history or Streamlit interface

---

## **5. Troubleshooting & Common Issues**

| Issue                    | Likely Cause                                        | Solution                                                           |
| ------------------------ | --------------------------------------------------- | ------------------------------------------------------------------ |
| `ModuleNotFoundError`    | Missing import or virtual environment               | Verify all dependencies installed and Python environment activated |
| Agent.run() fails        | Tool not registered or code error                   | Check `initialize_agent` registration and function definitions     |
| Vector store not loading | `persist_dir` incorrect or Day 1 embeddings missing | Verify directory and re-run Day 1 embedding steps                  |
| Flask server error       | Incorrect folder structure                          | Ensure `templates/` folder exists and contains `index.html`        |
| Gemini API errors        | Invalid or missing key                              | Verify `.env` configuration and key validity                       |

---

## **6. Learner Support Tips**

* Encourage learners to **test queries in Python REPL** first
* Show **verbose output** to help debug agent reasoning
* Ask learners to **explain errors in their own words** before fixing
* Highlight **modularity**, so they can isolate problems to RAG, tools, or frontend

---

## **7. Lab Assessment Criteria**

* Frontend successfully accepts and submits queries
* Backend agent returns correct responses with RAG + tools
* Tools execute correctly when invoked
* Learners can troubleshoot common issues
* Optional: Learners extend app with additional tools or chat history

---

## **8. Key Takeaways to Reinforce**

* Frontend + RAG + Agent integration = interactive AI assistant
* Modular design allows **easy enhancements** and **scalability**
* Debugging involves **checking each layer separately**: Frontend → Agent → RAG → Tools
* Learners now have a **fully working AI application** ready for deployment or further extension

---

This guide equips instructors to **deliver Day 3 effectively**, support learners in building their final AI application, and troubleshoot common issues.

---

