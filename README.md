# 🚀 Brand Guardian AI

**Video Compliance Auditing Pipeline for Marketing Content**

Brand Guardian AI is a production-oriented pipeline that audits marketing videos for compliance violations using multimodal analysis (speech + OCR) and LLM reasoning.

It ingests a YouTube video, extracts textual signals via Azure Video Indexer, retrieves relevant policy rules using vector search, and generates a structured **PASS/FAIL compliance report**.

---

## 🔥 Key Features

* 🎥 **YouTube Video Ingestion**
* 🧠 **Multimodal Extraction**

  * Speech-to-text (transcript)
  * OCR (on-screen text)
* 🔍 **Semantic Policy Retrieval**

  * Azure AI Search (vector + keyword hybrid)
* 🤖 **LLM-Based Compliance Analysis**

  * Structured JSON outputs (strict schema)
* ⚡ **Dual Interface**

  * CLI + FastAPI API

## ⚙️ Architecture Diagram

<img width="1301" height="878" alt="Architecture Diagram" src="https://github.com/user-attachments/assets/bf2255f4-5b62-4e17-b516-f0767ddcbf21" />

---

## ⚙️ Tech Stack

| Layer            | Technology                     |
| ---------------- | ------------------------------ |
| API              | FastAPI                        |
| Workflow Engine  | LangGraph                      |
| LLM              | Groq (LLaMA 3.1)               |
| Retrieval        | Azure AI Search                |
| Embeddings       | Sentence Transformers (MiniLM) |
| Video Processing | Azure Video Indexer + yt-dlp   |
| Auth             | Azure Default Credentials      |
| Observability    | OpenTelemetry (Azure Monitor)  |
| Language         | Python 3.12+                   |

---

## 📂 Project Structure

```
ComplianceQAPipeline/
├── main.py                  # CLI entrypoint
├── backend/
│   ├── data/               # Policy documents
│   ├── scripts/            # Indexing pipeline
│   └── src/
│       ├── api/            # FastAPI server
│       ├── graph/          # LangGraph workflow
│       └── services/       # Azure integrations
```

---

## 🚀 How It Works

### 1. Video Processing

* Downloads video using `yt-dlp`
* Uploads to Azure Video Indexer
* Extracts:

  * Transcript
  * OCR text
  * Metadata

### 2. Retrieval

* Builds semantic query from extracted content
* Fetches top relevant compliance rules

### 3. LLM Audit

* Groq LLM evaluates content against rules
* Returns structured JSON with:

  * Final status (`PASS` / `FAIL`)
  * Violations with severity
  * Summary report

---

## 📡 API Usage

### POST `/audit`

**Request**

```json
{
  "video_url": "https://youtu.be/<id>"
}
```

**Response**

```json
{
  "session_id": "uuid",
  "video_id": "vid_xxx",
  "status": "PASS",
  "final_report": "Summary",
  "compliance_results": [
    {
      "category": "Claim Validation",
      "severity": "CRITICAL",
      "description": "Violation detail"
    }
  ]
}
```

---

## 💡 Engineering Highlights

* **Deterministic pipeline** using LangGraph (no agent randomness)
* **Strict JSON parsing** for reliable downstream consumption
* **Hybrid retrieval** improves factual grounding
* **Separation of concerns**:

  * ingestion → retrieval → reasoning
* Designed for **scalability & production extension**

---



## 🛣️ Future Improvements

* Async processing + job queue (Celery / Kafka)
* Docker + cloud deployment (Azure / AWS)
* Batch video auditing
* Real-time streaming compliance checks
* Dashboard for compliance analytics

---

## 👨‍💻 Use Cases

* Ad compliance validation (legal / regulatory)
* Brand safety monitoring
* Content moderation pipelines
* Marketing QA automation

---

## ⚡ System Highlights
This project demonstrates **real-world AI system design**, combining:

* Multimodal data processing
* Retrieval-Augmented Generation (RAG)
* Production-grade API architecture
* Cloud-native integrations


---

