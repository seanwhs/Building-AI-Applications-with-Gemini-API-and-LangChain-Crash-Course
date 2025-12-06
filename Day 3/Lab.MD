# **Day 3 Lab — Frontend Integration & Final AI Application**

**Duration:** 3–4 hours
**Objective:** Integrate your RAG + Agent backend with a simple frontend to create a working AI assistant.

---

## **Lab Prerequisites**

* Completion of **Day 1 & Day 2 labs**
* Python 3.10+ installed
* Gemini API key configured in `.env`
* Dependencies installed (`pip install -r requirements.txt`)
* Basic understanding of Flask (or Streamlit)

---

## **Lab Goals**

By the end of this lab, learners will:

1. Set up a frontend interface for AI queries
2. Connect frontend to backend (RAG + Agents + Tools)
3. Test multi-step queries with the AI assistant
4. Optionally enhance the app with multiple tools or chat history

---

## **Lab Steps**

### **Step 1 — Setup Project Structure**

Create the following structure if not already present:

```
project_root/
│
├─ backend/       # RAG + Agent code
├─ frontend/      # Frontend code
├─ documents/     # Sample PDFs/TXT
├─ .env
├─ requirements.txt
└─ README.md
```

---

### **Step 2 — Frontend Setup (Flask)**

1. In `frontend/`, create `app.py`:

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

2. Create `templates/index.html`:

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

* Ensure your **agent** from Day 2 is accessible in `backend/agent_runner.py`
* Agent should already include:

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
* Test queries, for example:

  * `"What is RAG?"`
  * `"Calculate 15 * 12"`
  * `"Explain embeddings and calculate 8*8"`

**Observe:**

* The AI returns document-based answers
* Tools execute correctly
* Agent reasoning is visible if `verbose=True`

---

### **Step 5 — Lab Challenges / Optional Enhancements**

1. **Add multiple tools:**

   * Web search tool, date/time tool, unit converter, etc.
2. **Chat history:**

   * Maintain previous queries and responses in the session
3. **Improve UI:**

   * Use CSS or integrate Streamlit for a more modern look
4. **Deployment:**

   * Dockerize the app
   * Deploy locally or on cloud platforms

---

### **Step 6 — Lab Checklist**

* [ ] Frontend displays a text input form
* [ ] Queries sent to agent return valid answers
* [ ] RAG chain returns relevant document context
* [ ] Tools execute correctly (calculations, API calls)
* [ ] Application is modular and ready for future extensions

---

### **Tips & Troubleshooting**

| Issue                  | Solution                                                   |
| ---------------------- | ---------------------------------------------------------- |
| Agent.run() fails      | Check tool registration and imports                        |
| Vector store not found | Ensure `persist_dir` is correct and Day 1 embeddings exist |
| API errors             | Verify Gemini API key in `.env`                            |
| Flask server errors    | Ensure correct directory and `templates/` folder           |

---

This lab ensures learners **finish the full AI application** by integrating **backend reasoning, document retrieval, and tools** with a **frontend interface**.

---

