# **Day 3 Quiz — Frontend Integration & Final AI Application**

**Instructions:** Choose the correct answer(s) or write a short answer.

---

### **Multiple Choice**

1. What is the primary purpose of integrating a frontend with your AI backend?
   a) To store embeddings
   b) To allow users to interact with the AI via a user interface
   c) To train the LLM
   d) To persist vector stores

**Answer:** b

2. In Flask, which folder is required to store HTML templates?
   a) static
   b) templates
   c) frontend
   d) backend

**Answer:** b

3. What does the agent do in a LangChain RAG + Tools setup?
   a) Only retrieves documents
   b) Performs reasoning, executes tools, and generates responses
   c) Stores vector embeddings
   d) Hosts the frontend server

**Answer:** b

4. Which of the following are valid troubleshooting steps if `agent.run()` fails?
   a) Check tool registration
   b) Verify Gemini API key
   c) Reboot the computer
   d) Ensure backend modules are correctly imported

**Answer:** a, b, d

---

### **Short Answer**

5. Explain the flow of a user query through the frontend to the backend agent in your AI assistant.

**Sample Answer:**

* User submits a query via the frontend form → Frontend sends the query to the backend agent → Agent retrieves relevant document chunks via RAG → Agent executes tools if needed → Agent generates response → Response sent back to frontend → Displayed to user.

6. Name two optional enhancements you can add to the AI assistant.

**Sample Answers:**

* Multiple tools (e.g., web search, calculator)
* Chat history
* UI improvements with CSS or Streamlit
* Deployment using Docker or cloud services

7. If the vector store is not found, what is a possible cause and solution?

**Sample Answer:**

* Cause: Day 1 embeddings were not persisted or `persist_dir` path is incorrect
* Solution: Verify the directory path and regenerate embeddings if needed

---

# **Day 3 Detailed Notes**

### **1. Frontend Overview**

* **Purpose:** Provide a user-friendly interface to submit queries to the AI backend
* **Options:** Flask (simpler for HTML forms) or Streamlit (interactive, modern UI)
* **Flow:** User input → Frontend → Backend agent → RAG + Tools → Response → Frontend display

---

### **2. Backend Integration**

* **Agent:** Combines RAG chain + tools to generate multi-step answers
* **RAG Chain:** Retrieves document context for user queries
* **Tools:** Calculator, API fetchers, or custom functions
* **Integration:** Frontend calls `agent.run(query)` and displays the response

---

### **3. Running the Application**

* Start frontend: `python app.py`
* Open `http://127.0.0.1:5000/`
* Test queries with combinations of document questions and tool calls
* Observe agent reasoning if `verbose=True`

---

### **4. Optional Enhancements**

* **Multiple Tools:** Allow agent to perform more than one type of task
* **Chat History:** Maintain prior queries and responses for context
* **UI Improvements:** Add CSS styling or switch to Streamlit for richer interface
* **Deployment:** Docker, Heroku, or Streamlit Cloud

---

### **5. Troubleshooting Tips**

* **Agent.run() fails:** Check tool registration and imports
* **Vector store missing:** Verify `persist_dir` and that embeddings exist
* **Flask server errors:** Ensure folder structure is correct (`templates/` for HTML)
* **Gemini API errors:** Check API key in `.env`

---

### **6. Key Takeaways**

* Frontend + Backend integration makes the AI assistant **interactive and usable**
* RAG + Tools + Agent = **powerful, multi-step reasoning system**
* Modular design allows for **extensibility and deployment**
* Debugging requires checking **each layer independently**

---

This completes the **Day 3 course materials**, including:

* README
* Lab Instructions
* Slide Deck
* Lesson Plan
* Learner Guide
* Trainer Guide
* Quiz
* Detailed Notes

---

