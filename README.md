# Clara AI Automation Pipeline

## Overview
This project implements an **automation pipeline** that converts customer conversations into deployable AI voice agents for **Clara Answers**.

The system processes two types of inputs:

Demo Call → Agent Draft (v1)  
Onboarding Call → Agent Update (v2)

The pipeline extracts operational rules from transcripts and generates **structured configurations for AI voice agents**.

This solution meets the assignment requirements for:

- Zero-cost tooling
- Structured data extraction
- Versioned agent configuration
- Reproducible automation
- Batch processing

---

# System Architecture

```
                Demo Call Transcript
                        │
                        ▼
             Account Memo Extraction
                        │
                        ▼
              Retell Agent Draft (v1)
                        │
                        ▼
                Stored in Repository


           Onboarding Call Transcript
                        │
                        ▼
                Update Extraction
                        │
                        ▼
            Updated Account Memo (v2)
                        │
                        ▼
              Updated Agent Spec
                        │
                        ▼
               Changelog (v1 → v2)
```

---

# Project Structure

```
clara-ai-assignment
│
├── data
│   ├── demo_calls
│   └── onboarding_calls
│
├── outputs
│   └── accounts
│       └── bens_electric_001
│           ├── v1
│           │   ├── account_memo.json
│           │   └── agent_spec.json
│           │
│           └── v2
│               ├── account_memo.json
│               ├── agent_spec.json
│               └── changes.md
│
├── scripts
│   ├── extract_memo.py
│   ├── extract_onboarding_updates.py
│   ├── generate_agent_spec.py
│   ├── generate_changelog.py
│   └── run_batch.py
│
├── workflows
│   ├── demo_to_v1.json
│   └── onboarding_to_v2.json
│
└── README.md
```

---

# Pipeline A — Demo Call → Agent v1

### Input
Demo call transcript

### Process

1. Extract structured account memo  
2. Generate Retell agent draft  
3. Store versioned configuration  

### Output

```
outputs/accounts/<account_id>/v1/account_memo.json
outputs/accounts/<account_id>/v1/agent_spec.json
```

---

# Pipeline B — Onboarding Call → Agent v2

### Input
Onboarding call transcript

### Process

1. Extract configuration updates  
2. Patch the **v1 account memo**  
3. Generate updated agent spec  
4. Produce a changelog  

### Output

```
outputs/accounts/<account_id>/v2/account_memo.json
outputs/accounts/<account_id>/v2/agent_spec.json
outputs/accounts/<account_id>/v2/changes.md
```

---

# Running the Pipeline

Run the full pipeline using the batch script:

```
python scripts/run_batch.py
```

This will automatically process:

Demo Call → Agent v1  
Onboarding Call → Agent v2  
Generate Changelog

---

# n8n Workflow

Two workflow automations are included:

```
workflows/demo_to_v1.json
workflows/onboarding_to_v2.json
```

These workflows orchestrate the pipeline by triggering the Python scripts and managing the processing flow.

---

# Zero-Cost Implementation

This project uses only **free tools**:

| Tool | Purpose |
|-----|--------|
| Python | Core automation scripts |
| Local file storage | Data persistence |
| n8n (Docker) | Workflow orchestration |
| Whisper / free transcription | Audio transcription |

No paid APIs or services were used.

---

# Known Limitations

- CRM integrations are mocked (Jobber integration not yet available)
- Emergency routing rules depend on transcript clarity
- Transcription accuracy may affect extraction results

---

# Future Improvements

With production access the system could be expanded to include:

- Automated speech-to-text pipeline
- Structured database storage (Supabase)
- Direct Retell API agent creation
- Web dashboard for account configuration
- Automated prompt QA validation

---

# Demo

A short Loom walkthrough demonstrates:

- Running the pipeline
- Generated outputs
- Version updates from **v1 → v2**

---

# Author

Automation pipeline developed as part of the **Clara Answers Intern Engineering Assignment**.
