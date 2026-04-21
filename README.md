# 🤖 NISTBot — NIST SP 800-53 Compliance Chatbot

## 🚀 Live Demo
👉 [Try NISTBot](https://funkeomolere.github.io/nistbot)

A RAG-powered AI chatbot that answers questions against NIST SP 800-53 Rev 5 documentation. Built as a practical GRC learning project using N8N, Pinecone, OpenAI, Google Cloud, and Anthropic.

---

## What It Does

NISTBot lets you query the full NIST SP 800-53 Rev 5 control framework in plain English. Instead of manually searching through hundreds of pages of documentation, you ask a question and the bot retrieves the most relevant controls and explains them clearly.

**Example queries:**
- *"What are the access control requirements under AC-2?"*
- *"What does NIST say about incident response planning?"*
- *"Which controls apply to audit logging?"*

---

## 🏗️ Architecture

The project is built on a **RAG (Retrieval-Augmented Generation)** pipeline split across two N8N workflows:

```
┌─────────────────────────────────────────────────────┐
│              WORKFLOW 1: Document Ingestion          │
│                                                     │
│  Google Drive → Download PDF → Chunk Text →         │
│  Generate Embeddings (OpenAI) → Store in Pinecone   │
└─────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────┐
│              WORKFLOW 2: AI Chat Agent               │
│                                                     │
│  User Query → Embed Query → Search Pinecone →       │
│  Retrieve Relevant Chunks → Claude AI Response      │
└─────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Platform | Role |
|---|---|
| **N8N** | Workflow automation (orchestrates the full pipeline) |
| **Pinecone** | Vector database (stores and retrieves document embeddings) |
| **OpenAI** | Embeddings model (`text-embedding-3-small`) |
| **Google Cloud / Drive** | Document storage (NIST SP 800-53 Rev 5 PDF) |
| **Anthropic Claude** | AI language model (generates answers) |

---

## 📁 Repository Structure

```
├── workflow-ingestion.json     # N8N: Document ingestion pipeline
├── workflow-chatbot.json       # N8N: AI Agent chat interface
└── README.md
```

---

## ⚙️ Configuration

### Pinecone
- Index name: `chat`
- Dimensions: `1536`
- Metric: `cosine`
- Namespace: `nistbot`

### OpenAI
- Embedding model: `text-embedding-3-small`

### Google Drive
- Source folder: `policy`
- Document: NIST SP 800-53 Rev 5 (PDF)

> **Note:** API keys and credentials are stored in N8N's credential store and are **not** included in the exported workflow JSON files.

---

## 🚀 How to Use

1. Import both workflow JSON files into your N8N instance
2. Set up credentials in N8N for: OpenAI, Pinecone, Google Drive, and Anthropic
3. Run **Workflow 1** to ingest and embed the NIST document into Pinecone
4. Activate **Workflow 2** to enable the chat interface
5. Send queries via the webhook endpoint

---

## 📚 Source Document

- **NIST Special Publication 800-53 Revision 5**
  Security and Privacy Controls for Information Systems and Organizations
  [Download from NIST](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final)

---

## About This Project

This project was built as part of a hands-on GRC learning session led by **James Tabron**, exploring how AI and automation tools can support compliance workflows. It demonstrates practical application of RAG architecture for navigating complex regulatory documentation.

---

## 📄 License

This project is for educational and portfolio purposes.
