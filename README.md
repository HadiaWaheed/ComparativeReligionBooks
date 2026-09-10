# 📚 Comparative Religion AI Assistant

An AI-powered **RAG (Retrieval-Augmented Generation)** assistant built on top of a curated collection of comparative religion and Islamic books.

The project allows users to ask questions about the books and receive AI-generated answers based on relevant information retrieved directly from the book collection.

---

## ✨ About the Project

**Comparative Religion AI Assistant** combines a digital book library with Artificial Intelligence, Natural Language Processing, embeddings, vector search, and Large Language Models.

Instead of sending a user's question directly to an AI model, the system first searches the available books for relevant content. The retrieved information is then provided to the AI model as context.

This approach helps generate answers that are grounded in the available source material.

---

## 🧠 How It Works

```text
User asks a question
        ↓
Question is converted into an embedding
        ↓
FAISS searches for relevant book sections
        ↓
Relevant text chunks are retrieved
        ↓
Retrieved content is sent to the AI model
        ↓
AI generates an answer
        ↓
Answer and book sources are displayed
````

---

## 🏗️ Project Structure

```text
ComparativeReligionBooks/
│
├── 📁 library/
│   ├── islam/
│   ├── christianity/
│   ├── comparative-religion/
│   ├── philosophy/
│   └── ...
│
├── 📁 rag/
│   ├── ingest.py
│   ├── retriever.py
│   ├── generator.py
│   └── requirements.txt
│
├── 📁 backend/
│   ├── app.py
│   └── config.py
│
├── 📁 frontend/
│   ├── home.html
│   ├── style.css
│   └── script.js
│
├── 📁 data/
│   ├── chunks.json
│   └── index.faiss
│
├── .env
├── .gitignore
└── README.md
```

> The generated files inside `data/` are created locally during the RAG ingestion process and are excluded from Git tracking.

---

## 🔧 Technologies Used

* **Python** – Core programming language
* **FastAPI** – Backend API
* **Sentence Transformers** – Text embeddings
* **FAISS** – Vector similarity search
* **PyPDF** – PDF text extraction
* **NumPy** – Numerical processing
* **Google Gemini API** – AI answer generation
* **HTML** – Frontend structure
* **CSS** – Frontend styling
* **JavaScript** – Frontend interaction

---

## 🔍 RAG Pipeline

### 1. PDF Ingestion

The `rag/ingest.py` script scans the `library/` directory and processes the available PDF books.

It:

* Finds PDF files recursively
* Extracts text from PDFs
* Splits the text into smaller chunks
* Generates vector embeddings
* Creates a FAISS vector index
* Saves the processed chunks locally

---

### 2. Text Embeddings

The project uses the **Sentence Transformers** model:

```text
all-MiniLM-L6-v2
```

The model converts text into numerical vectors called embeddings.

These embeddings allow the system to find text that is semantically similar to the user's question.

---

### 3. Vector Search

The project uses **FAISS** to perform similarity search.

When a user asks a question, the system searches the vector index and retrieves the most relevant sections from the available books.

The retriever currently returns the top relevant chunks from the collection.

---

### 4. AI Answer Generation

The retrieved book content is passed to the **Google Gemini API** as source material.

The AI is instructed to:

* Use the provided source material
* Avoid inventing books, quotes, or references
* Clearly indicate when the source material is insufficient
* Provide a helpful and concise answer
* Respect different religious viewpoints

---

## ⚙️ Backend

The backend is built using **FastAPI**.

The main API endpoint is:

```text
POST /ask
```

Example request:

```json
{
  "question": "What does the book say about Islam?"
}
```

The backend:

1. Receives the user's question
2. Searches the RAG index
3. Retrieves relevant book content
4. Sends the context to Gemini
5. Returns the generated answer
6. Returns the relevant book sources

---

## 🖥️ Frontend

The project includes a simple web-based AI chat interface.

Users can:

* Ask questions about the books
* Receive AI-generated answers
* View relevant sources
* Use quick question prompts
* Interact with the assistant through a chat-style interface

The frontend communicates with the FastAPI backend through the `/ask` API endpoint.

---

## 🚀 Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/SENODROOM/ComparativeReligionBooks.git
cd ComparativeReligionBooks
```

---

### 2. Install Python Dependencies

The project uses Python 3.13.

Install the required packages:

```bash
pymanager exec -3.13 -m pip install -r rag/requirements.txt
```

---

### 3. Configure Gemini API

Create a `.env` file in the project root:

```env
GEMINI_API_KEY=YOUR_API_KEY
```

Replace `YOUR_API_KEY` with your Google Gemini API key.

**Never expose your API key in frontend files or commit the `.env` file to GitHub.**

---

### 4. Build the RAG Index

Run:

```bash
pymanager exec -3.13 rag/ingest.py
```

This processes the books and creates the local RAG data:

```text
data/chunks.json
data/index.faiss
```

---

### 5. Start the Backend

Run:

```bash
pymanager exec -3.13 -m uvicorn backend.app:app --reload
```

The backend will run at:

```text
http://127.0.0.1:8000
```

---

### 6. Start the Frontend

Open another terminal:

```bash
cd frontend
pymanager exec -3.13 -m http.server 5501
```

Then open:

```text
http://127.0.0.1:5501/home.html
```

---

## 📖 Book Library

The `library/` directory contains PDF books organized into different categories.

Examples include:

```text
library/
├── islam/
├── christianity/
├── comparative-religion/
├── philosophy/
└── other-topics/
```

The library can be expanded with additional relevant books.

---

## 🔐 Security

The Gemini API key is stored in the backend `.env` file.

The API key is not included in frontend JavaScript.

The following generated files are ignored by Git:

```text
.env
data/chunks.json
data/index.faiss
__pycache__/
*.pyc
```

This prevents sensitive information and large generated files from being accidentally committed.

---

## 🎯 Project Goals

The main goals of this project are to:

* Make a large collection of books easier to explore
* Provide AI-assisted research
* Retrieve relevant information from books
* Generate answers grounded in source material
* Display relevant book sources
* Demonstrate a practical RAG and LLM application
* Combine traditional digital libraries with modern AI technology

---

## 🌟 Key Features

* 📚 PDF-based knowledge library
* 🔎 Semantic search
* 🧠 AI-powered question answering
* ⚡ FAISS vector retrieval
* 🤖 Google Gemini integration
* 🔗 Source-aware responses
* 🌐 FastAPI backend
* 💻 Interactive web frontend
* 🔐 Environment-based API key protection

---

## ⚠️ Disclaimer

This project is intended for educational and research purposes.

AI-generated answers should be checked against the original books and source material, especially when dealing with religious, historical, or scholarly topics.

The assistant should not be treated as a replacement for qualified scholars, researchers, or primary sources.

---

## 👩‍💻 Project Stack

```text
PDF Books
   ↓
PyPDF
   ↓
Text Chunking
   ↓
Sentence Transformers
   ↓
FAISS Vector Database
   ↓
FastAPI
   ↓
Google Gemini
   ↓
Web Chat Interface
```

---

## 📌 Future Improvements

Possible future improvements include:

* Better document metadata
* Page-level citations
* Improved source highlighting
* Book and author filters
* Multi-language support
* Conversation history
* Advanced semantic search
* More efficient document processing
* Improved answer evaluation

---

## ⭐ Conclusion

**Comparative Religion AI Assistant** demonstrates how a traditional digital book collection can be transformed into an interactive AI-powered knowledge system using **RAG, embeddings, vector search, FastAPI, and Google Gemini**.

The project provides a foundation for building a reliable AI research assistant grounded in a curated collection of books.
