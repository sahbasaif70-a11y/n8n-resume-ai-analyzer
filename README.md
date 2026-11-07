# 🤖 n8n Resume AI Analyzer & Candidate Screening Automation

An end-to-end automated recruitment pipeline built using **n8n**, **OpenAI (`gpt-4o`)**, **Gmail API**, **Google Drive API**, and **Google Sheets API**.

This project automatically processes incoming candidate resumes sent via email, archives them to Google Drive, extracts plain text from PDFs, evaluates candidate qualifications against a specific Job Description using an AI Agent, logs candidates into Google Sheets, and sends a personalized HTML assessment report back to candidates.

---

## 🏗️ Architecture & Workflow Pipeline

```
[Gmail Trigger] ➡️ [Upload File to Drive] ➡️ [Download File] ➡️ [Extract Text from PDF]
                                                                        │
                                                                        ▼
                                                           [Information Extractor] ◄──┐
                                                                        │             │ (OpenAI gpt-4o)
                                                                        ▼             │
                                                                   [AI Agent] ────────┘
                                                                        │
                                                                        ▼
                                                                  [Edit Fields]
                                                                        │
                                                                        ▼
                                                             [JavaScript Code Parser]
                                                                        │
                                                                        ▼
                                                              [Append Row in Sheet]
                                                                        │
                                                                        ▼
                                                                [IF Guard Rail]
                                                                 (score >= 4)
                                                                        │ (True)
                                                                        ▼
                                                             [Build Email Content]
                                                                        │
                                                                        ▼
                                                                [Send HTML Email]
```

---

## ✨ Features

- 📧 **Automated Gmail Ingestion**: Polls inbox for incoming application emails with PDF attachments.
- 📁 **Cloud Archiving**: Archives received CVs to a dedicated Google Drive folder (`Job Resumes`).
- 🧠 **Structured Entity Extraction**: Uses OpenAI structured JSON output to parse candidate contact details (`Name`, `Email`, `Phone Number`).
- 🤖 **AI Candidate Scoring**: Evaluates candidate experience, education, and skill set against job requirements for a *Junior AI Automation Engineer*, assigning a relevance score (`1–10`) and justification.
- 🧹 **Robust Output Parsing**: JavaScript Code node with flexible regex handlers to parse free-form LLM outputs into clean JSON fields.
- 📊 **Google Sheets Logging**: Automatically appends candidate records into clean spreadsheet columns (`Resume Analyzer`).
- 🛡️ **Guard Rail Logic**: IF node condition ensures only candidates scoring 4/10 or above receive detailed HTML evaluation reports.
- 📩 **Personalized HTML Feedback**: Composes inline-styled HTML evaluation reports sent back to candidates directly.

---

## 🛠️ Tech Stack & Integrations

- **Workflow Engine**: n8n (Self-Hosted / Cloud)
- **LLM / AI Model**: OpenAI API (`gpt-4o`)
- **Google Cloud APIs**: Gmail API, Google Drive API, Google Sheets API
- **Scripting**: JavaScript (ES6+, Regex, HTML Template Literals)

---

## 📂 Project Structure

```
├── n8n_resume_ai_analyzer_workflow.json   # Exported n8n workflow JSON file
└── README.md                              # Detailed project documentation
```

---

## 🚀 How to Import & Run

1. **Clone or Download Repository**:
   ```bash
   git clone https://github.com/YOUR_USERNAME/n8n-resume-ai-analyzer.git
   ```

2. **Import into n8n**:
   - Open your n8n workspace (`http://localhost:5678`).
   - Click **Workflows** → **Import from File**.
   - Select `n8n_resume_ai_analyzer_workflow.json`.

3. **Set Up Credentials**:
   - **Gmail OAuth2 API**
   - **Google Drive OAuth2 API**
   - **Google Sheets OAuth2 API**
   - **OpenAI API Key** (`gpt-4o`)

4. **Prepare Google Assets**:
   - Create a Google Drive folder named `Job Resumes`.
   - Create a Google Sheet named `Resume Analyzer` with columns: `Name`, `Email`, `Number`, `Skill Set`, `Qualifications`, `Job History`, `Score`, `Justification`.

5. **Activate Workflow**:
   - Toggle the workflow to **Active** (Green).

---

## 📄 License
This project is open-source and available for educational and portfolio demonstration purposes.
