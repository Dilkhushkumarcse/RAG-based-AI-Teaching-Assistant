
---

# **RAG-Based AI Teaching Assistant**

A fully functional **Retrieval-Augmented Generation (RAG)** AI system designed to help users learn from **your own video lectures**.
This assistant converts videos → audio → transcripts → embeddings → intelligent answers.

It allows you to ask questions about your teaching content, and the AI responds using retrieved context from your videos.

---
## **Features**

* Process your own videos into structured learning data
* Automatic MP3 extraction
* JSON transcript generation
* Embedding creation using vector databases
* RAG-powered question answering
* Fast and scalable pipeline
* Easily extend or integrate with any LLM

---

## **Tech Stack**

* **Python**
* **Whisper / Speech-to-Text**
* **Sentence Transformers / Embedding Model (e.g., bge-m3)**
* **Pandas**
* **Joblib**
* **FAISS / Custom Vector Search**
* **Any LLM (GPT, Ollama, etc.)**

---

# **Project Workflow Overview**

The system works in **five major steps**:

---

# **Step 1 — Collect Your Videos**

Move all your lecture or tutorial videos into the folder:

```
/videos
```

Supported formats: **.mp4, .mkv, .mov, .avi**

---

# **Step 2 — Convert Videos to MP3**

Run:

```bash
python video_to_mp3.py
```

This will extract audio from every video and store it inside:

```
/audio
```

---

# **Step 3 — Convert MP3 to JSON Transcripts**

Run:

```bash
python mp3_to_json.py
```

This will generate:

```
/transcripts/filename.json
```

Each JSON contains:

```json
{
  "text": "... transcript text ...",
  "start_time": 0,
  "end_time": 120
}
```

---

# **Step 4 — Convert JSON to Embeddings (Vector Database)**

Run:

```bash
python preprocess_json.py
```

This script will:

* Read all JSON transcripts
* Split text into searchable chunks
* Generate embeddings
* Create a dataframe
* Save it as a `.joblib` file

Example output:

```
data/teaching_embeddings.joblib
```

---

# **Step 5 — RAG Pipeline (Prompt Generation + LLM)**

Use:

```python
df = joblib.load("data/teaching_embeddings.joblib")
```

Workflow:

1. Receive query from user
2. Convert it to an embedding
3. Perform similarity search
4. Extract top relevant transcript chunks
5. Construct a **RAG Prompt**:

```
Use the context below to answer the user's question.
Context:
<Most relevant chunks>

Question: <user_query>

Answer:
```

6. Send the prompt to the LLM (GPT/Ollama/etc.)
7. Return the final answer

---

# **Example RAG Prompt**

```
You are an AI Teaching Assistant. Use ONLY the context below to answer.

Context:
- Topic: HTML Basic Tags
- Video Timestamp: 02:10 – 02:43
"HTML uses tags such as <h1>, <p>, <a> to structure content…"

User Question:
"What tags are used for headings?"

Answer:
```

---

# **Project Structure**

```
rag-teaching-assistant/
│
├── videos/                 # Raw video files
├── audio/                  # Extracted mp3 files
├── embeddings.joblib
├── video_to_mp3.py
├── mp3_to_json.py
├── preprocess_json.py
├── process_incoming.py            # Main RAG QA script
│
└── README.md
```

---

# **How It Works (High-Level Flow)**

```
VIDEO → MP3 → TRANSCRIPT(JSON) → EMBEDDINGS → VECTOR SEARCH → RAG PROMPT → LLM ANSWER
```

This makes your AI assistant capable of deeply understanding **your teaching style**, **your examples**, and **your explanations**.

---

# **Future Improvements**

* Add a web UI for chatting
* Add timestamps & video playback links in responses
* Use FAISS for faster vector search
* Add quiz generation from videos
* Add multi-language support
* Integrate with Flask / FastAPI

---

# 👨‍💻**Author**

**Dilkhush Kumar**

AI/ML & Data Science Enthusiast | CSE Engineer
Building AI Teaching Systems & RAG Models

---
