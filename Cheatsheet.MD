# **Gemini API + LangChain Cheat Sheet**

---

## **1. Setup & Environment**

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate      # Linux/Mac
venv\Scripts\activate         # Windows

# Install dependencies
pip install langchain openai flask python-dotenv faiss-cpu
```

**Environment Variables (.env):**

```
GEMINI_API_KEY="your_api_key_here"
```

---

## **2. Key Concepts**

| Concept                                  | Description                                                         |
| ---------------------------------------- | ------------------------------------------------------------------- |
| **RAG (Retrieval-Augmented Generation)** | Retrieve relevant documents and combine with LLM reasoning          |
| **Embeddings**                           | Convert text into vector representations for semantic search        |
| **Agent**                                | LangChain object that can reason, execute tools, and answer queries |
| **Tools**                                | Functions the agent can call (calculator, API fetch, etc.)          |
| **Vector Store**                         | Database of embeddings for similarity search (e.g., FAISS)          |

---

## **3. Embeddings & Vector Store**

```python
from langchain.embeddings import OpenAIEmbeddings
from langchain.vectorstores import FAISS

# Create embeddings
embeddings = OpenAIEmbeddings()
vectorstore = FAISS.from_texts(["text1", "text2"], embeddings)

# Persist for reuse
vectorstore.save_local("persist_dir")
# Load later
vectorstore = FAISS.load_local("persist_dir", embeddings)
```

---

## **4. RAG Chain**

```python
from langchain.chains import RetrievalQA

# Setup retrieval-based QA
retriever = vectorstore.as_retriever()
qa_chain = RetrievalQA.from_chain_type(
    llm=gemini_llm,        # your LLM object
    chain_type="stuff",
    retriever=retriever
)

# Ask a question
answer = qa_chain.run("Explain embeddings")
```

---

## **5. Tools & Agents**

```python
from langchain.agents import Tool, initialize_agent
from langchain.chat_models import ChatOpenAI

# Example tool: calculator
def calc_tool(query):
    return str(eval(query))

tools = [Tool(name="Calculator", func=calc_tool, description="Performs math calculations")]

# Initialize agent
agent = initialize_agent(
    tools,
    llm=ChatOpenAI(temperature=0),
    agent="zero-shot-react-description",
    verbose=True
)

# Run query
response = agent.run("Calculate 12*12 and explain embeddings")
```

---

## **6. Frontend Integration (Flask Example)**

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

`index.html`:

```html
<form method="post">
    <input type="text" name="query" placeholder="Ask a question..." size="50"/>
    <button type="submit">Ask</button>
</form>
<p>{{ answer }}</p>
```

---

## **7. Debugging & Tips**

| Issue                  | Solution                                  |
| ---------------------- | ----------------------------------------- |
| `agent.run()` fails    | Check tool registration & imports         |
| Vector store not found | Verify `persist_dir` and embeddings exist |
| Flask template error   | Ensure `templates/index.html` exists      |
| API key issues         | Check `.env` and key validity             |

**Tips:**

* Use **verbose=True** for agents to see reasoning steps
* Test queries in **Python REPL** before connecting frontend
* Modular design: separate **RAG chain**, **tools**, and **frontend**

---

## **8. Optional Enhancements**

* Add multiple tools (search API, date/time, unit converter)
* Maintain **chat history** for contextual conversations
* Improve UI with CSS or switch to **Streamlit**
* Deploy via **Docker**, **Heroku**, or **Streamlit Cloud**

---

## **9. Quick Commands Summary**

```bash
# Run Flask frontend
python frontend/app.py

# Run Python agent test
python -c "from backend.agent_runner import agent; print(agent.run('Calculate 15*15'))"

# Recreate embeddings
python -c "from backend.embedding_setup import create_embeddings; create_embeddings()"
```

---

This cheat sheet is designed to give learners **instant access to essential commands, patterns, and best practices** for building AI applications using **Gemini API + LangChain**.

---

