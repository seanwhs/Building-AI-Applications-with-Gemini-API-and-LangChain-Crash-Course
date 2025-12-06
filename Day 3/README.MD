# **Day 3 README — Frontend Integration & Final Application**

### *Building AI Applications with Gemini API & LangChain*

---

## **Overview**

**Objective:**
On Day 3, we will:

* Integrate the **RAG + Agents backend** built in Day 2 with a **simple frontend**
* Build a **working AI assistant** capable of answering document-based questions and performing multi-step tasks
* Deploy a **local web application** for user interaction

**Outcome:**
By the end of Day 3, you will have a **fully functional AI application** combining:

* Document retrieval
* LLM-based answer generation
* Tools and agent reasoning
* Frontend interface

---

## **Prerequisites**

* Completion of Day 1 and Day 2 labs
* Python 3.10+ installed
* Gemini API key configured in `.env`
* Installed dependencies from `requirements.txt`

---

## **Directory Structure**

```
project_root/
│
├─ backend/
│   ├─ vector_store.py
│   ├─ rag_chain.py
│   ├─ tools.py
│   ├─ agent_runner.py
│   └─ utils.py
│
├─ frontend/
│   ├─ app.py
│   ├─ templates/
│   │   └─ index.html
│   └─ static/
│       └─ styles.css
│
├─ documents/
│   └─ sample.pdf
│
├─ .env
├─ requirements.txt
└─ README.md
```

---

## **Step 1 — Install Dependencies**

```bash
pip install -r requirements.txt
```

Dependencies include:

* `langchain`
* `chromadb`
* `langchain-google-genai`
* `flask` (or `streamlit` if preferred)

---

## **Step 2 — Backend Overview**

**Components:**

1. **Vector Store** (`vector_store.py`)

   * Loads persisted embeddings from Day 1

2. **RAG Chain** (`rag_chain.py`)

   * Retrieves document chunks and generates answers using Gemini LLM

3. **Tools** (`tools.py`)

   * Custom tools (e.g., Calculator, API fetchers)

4. **Agent Runner** (`agent_runner.py`)

   * Initializes agent with tools
   * Executes queries combining RAG context and tools

**Example Usage:**

```python
from backend.rag_chain import rag_chain
from backend.agent_runner import agent

query = "What is the purpose of embeddings and calculate 12*12"
response = agent.run(query)
print(response)
```

---

## **Step 3 — Frontend Setup**

* Using **Flask** (or optionally Streamlit) for local UI
* `frontend/app.py`:

```python
from flask import Flask, render_template, request
from backend.agent_runner import agent

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

* `templates/index.html` (basic form):

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

## **Step 4 — Running the Application**

```bash
cd frontend
python app.py
```

* Open your browser at `http://127.0.0.1:5000/`
* Enter a query (e.g., `"Explain embeddings and calculate 15*15"`)
* Observe **context-aware answers + agent computation**

---

## **Step 5 — Optional Enhancements**

* Add **multiple tools** (web search, translation, weather API)
* Style the frontend with CSS or integrate Streamlit
* Add **chat history** to maintain context between queries
* Deploy using **Docker**, **Heroku**, or **Streamlit Cloud**

---

## **Step 6 — Key Points**

* Backend handles **document retrieval, reasoning, and tool execution**
* Frontend provides **user-friendly interface**
* Combining RAG + Agents ensures **accurate, multi-step responses**
* Modular structure makes it **easy to extend and scale**

---

## **Milestones for Day 3**

1. Frontend running and accepting user queries
2. RAG chain returns relevant document context
3. Tools execute correctly when invoked by agent
4. Agent produces multi-step, reasoned answers
5. Application is modular and ready for deployment

---

This README sets up learners to **launch a working AI assistant** and prepares them for **final project completion**.

---
