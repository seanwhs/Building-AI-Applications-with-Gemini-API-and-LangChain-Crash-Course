# **Day 3 Learner Guide — Frontend Integration & Final AI Application**

### *Gemini API + LangChain Crash Course*

---

## **1. Overview**

**Objective:**
On Day 3, you will integrate the **RAG + Agent backend** built in Days 1–2 with a frontend interface to create a **working AI assistant**.

**Learning Outcomes:**
By the end of the day, you will be able to:

1. Set up a frontend interface for AI queries
2. Connect frontend to the RAG + Agent backend
3. Test multi-step queries with document retrieval and tools
4. Troubleshoot frontend-backend integration issues
5. Optionally enhance the application with additional tools or chat history

---

## **2. Prerequisites**

* Completion of **Day 1 & Day 2 labs**
* Python 3.10+ installed
* Gemini API key configured in `.env`
* Installed dependencies (`pip install -r requirements.txt`)
* Basic understanding of Flask or Streamlit

---

## **3. Day 3 Schedule**

| Time      | Topic                 | Activity                                         |
| --------- | --------------------- | ------------------------------------------------ |
| 0:00–0:15 | Welcome & Recap       | Review RAG, Tools, Agents                        |
| 0:15–0:45 | Frontend Overview     | Introduction to Flask/Streamlit integration      |
| 0:45–1:30 | Frontend Setup        | Live coding: create basic UI for AI queries      |
| 1:30–2:15 | Backend Integration   | Connect frontend to RAG + Agent backend          |
| 2:15–3:00 | Lab Session           | Hands-on integration and testing                 |
| 3:00–3:15 | Break                 | Q&A and discussion                               |
| 3:15–4:00 | Optional Enhancements | Multi-tool agents, chat history, UI improvements |
| 4:00–4:30 | Testing & Debugging   | Troubleshoot issues and verify responses         |
| 4:30–4:45 | Wrap-up & Reflection  | Review milestones and next steps                 |

---

## **4. Lab Instructions**

### **Step 1 — Project Setup**

Ensure your project has the following structure:

```
project_root/
├─ backend/       # RAG + Agent code
├─ frontend/      # Frontend code
├─ documents/     # Sample PDFs/TXT
├─ .env
├─ requirements.txt
└─ README.md
```

---

### **Step 2 — Frontend Setup**

1. **Create `frontend/app.py`:**

```python
from flask import Flask, render_template, request
from backend.agent_runner import agent  # Import your agent from Day 2

app = Flask(__name__)

@app.route("/", methods=["GET", "POST"])
def index():
    answer = ""
    if request.method == "POST":
        query = request.form["query"]
        answer = agent.run(query)
    return render_template("index.html", answer=answer)

if __name__ == "__main__":
    app.run(debug=True)
```

2. **Create `templates/index.html`:**

```html
<!DOCTYPE html>
<html>
<head>
    <title>AI Assistant</title>
</head>
<body>
    <h1>AI Assistant</h1>
    <form method="post">
        <input type="text" name="query" placeholder="Ask a question..." size="50"/>
        <button type="submit">Ask</button>
    </form>
    <p>{{ answer }}</p>
</body>
</html>
```

---

### **Step 3 — Connect Frontend to Backend**

* Ensure your **agent** from Day 2 is accessible
* Agent should include:

  * RAG chain (`rag_chain`)
  * Tools (e.g., Calculator)
  * Agent initialization (`initialize_agent`)

**Test in Python first:**

```python
from backend.agent_runner import agent
response = agent.run("Explain embeddings and calculate 12*12")
print(response)
```

---

### **Step 4 — Run Frontend**

```bash
cd frontend
python app.py
```

* Open `http://127.0.0.1:5000/` in a browser
* Test queries:

  * `"What is RAG?"`
  * `"Calculate 15 * 12"`
  * `"Explain embeddings and calculate 8*8"`

**Observe:**

* Document-based answers
* Tool execution (calculations, API calls)
* Agent reasoning if `verbose=True`

---

### **Step 5 — Optional Enhancements**

1. **Add multiple tools:** Search API, translation, date/time calculator
2. **Chat history:** Maintain previous queries and responses
3. **Improve UI:** Add CSS or switch to Streamlit
4. **Deployment:** Dockerize or deploy on cloud platforms

---

### **Step 6 — Troubleshooting Tips**

| Issue                  | Solution                                                |
| ---------------------- | ------------------------------------------------------- |
| Agent.run() fails      | Check tool registration and imports                     |
| Vector store not found | Verify `persist_dir` and that Day 1 embeddings exist    |
| API errors             | Check Gemini API key in `.env`                          |
| Flask server errors    | Ensure correct directory and `templates/` folder exists |

---

### **Step 7 — Lab Checklist**

* [ ] Frontend accepts user queries
* [ ] Backend agent processes queries correctly
* [ ] RAG chain retrieves relevant document chunks
* [ ] Tools execute successfully when called by agent
* [ ] Application modular and ready for future extensions

---

## **7. Key Takeaways**

* Frontend integration allows **interactive AI applications**
* RAG + Agents + Tools = powerful reasoning assistant
* Modular design makes your application **extendable and scalable**
* Optional enhancements can **improve user experience and functionality**

---

This learner guide provides **step-by-step instructions, code snippets, and troubleshooting tips** to ensure learners complete the final AI application successfully.

---

