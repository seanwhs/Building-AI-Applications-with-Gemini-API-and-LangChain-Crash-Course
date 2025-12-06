# **Day 1 Quiz — Foundations & Document Pipeline**

**Instructions:**

* Total time: 20–25 minutes
* Answer all questions
* No external resources unless instructed

---

## **Section 1 — Multiple Choice (1 point each)**

**1. What is the main purpose of chunking documents when using LLMs?**
a) To reduce disk space usage
b) To split content into manageable pieces for the model
c) To increase the model’s output tokens
d) To automatically summarize the document

**Answer:** b

---

**2. Which LangChain component is responsible for embedding documents?**
a) TextSplitter
b) Retriever
c) Embeddings class (e.g., GoogleGenerativeAIEmbeddings)
d) Agent

**Answer:** c

---

**3. What type of data structure does a vector store (like Chroma) store?**
a) Raw PDFs only
b) Text strings
c) Numeric vectors representing semantic content
d) Python dictionaries

**Answer:** c

---

**4. Which of the following is NOT an advantage of using Gemini embeddings?**
a) Captures semantic meaning of text
b) Generates images from text
c) Enables similarity searches
d) Supports multimodal content

**Answer:** b

---

**5. In LangChain, which component is responsible for finding the most relevant chunks from a vector database?**
a) LLM
b) Retriever
c) TextSplitter
d) Config module

**Answer:** b

---

## **Section 2 — True / False (1 point each)**

**6. You must always manually split documents before embedding; LangChain cannot help with this.**

* True
* False

**Answer:** False

---

**7. Increasing chunk size may cause your LLM context window to overflow.**

* True
* False

**Answer:** True

---

**8. Chroma vector stores are persistent and can be saved to disk for later use.**

* True
* False

**Answer:** True

---

**9. Gemini embeddings can only be used with English text.**

* True
* False

**Answer:** False

---

**10. The similarity search function returns the chunks most semantically related to the query.**

* True
* False

**Answer:** True

---

## **Section 3 — Short Answer (2 points each)**

**11. Explain in your own words why embeddings are important in a RAG system.**

**Suggested Answer:**
Embeddings convert text into numeric vectors that capture semantic meaning, allowing the system to find and retrieve content relevant to a user’s query.

---

**12. Describe the purpose of `RecursiveCharacterTextSplitter`.**

**Suggested Answer:**
It splits large documents into smaller overlapping chunks, ensuring that each chunk fits within the LLM’s token limit and preserves context for better retrieval.

---

**13. What is the role of the `.env` file in Day 1’s project setup?**

**Suggested Answer:**
The `.env` file stores sensitive information like the Gemini API key, keeping it secure and allowing the code to access the API without hardcoding credentials.

---

**14. What is the difference between a document loader and a vector store?**

**Suggested Answer:**
A document loader reads and imports text from files (PDF, TXT, etc.), while a vector store stores the embeddings of these chunks for fast semantic search.

---

**15. Give one example of how changing the chunk size might affect retrieval quality.**

**Suggested Answer:**
Smaller chunks may improve relevance for fine-grained questions but increase the number of chunks to search, while larger chunks may include more context but risk overflowing the LLM context window or reducing precision.

---

**Scoring:**

* Multiple Choice: 5 points
* True/False: 5 points
* Short Answer: 10 points
* **Total: 20 points**

