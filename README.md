Clara AI Automation Pipeline
Overview

This project implements an automation pipeline that converts customer conversations into deployable AI voice agents for Clara Answers.

The system processes:

Demo Call → Agent Draft (v1)
Onboarding Call → Agent Update (v2)

It automatically extracts operational rules from transcripts and generates structured configurations for AI voice agents.

The solution follows the assignment requirements for:

Zero cost tooling

Structured data extraction

Versioned agent configuration

Reproducible automation

Batch processing

System Architecture
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
Updated Retell Agent Spec
        │
        ▼
Changelog (v1 → v2)
Project Structure
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
Pipeline A — Demo Call → Agent v1

Input:

Demo call transcript

Process:

Extract structured account memo

Generate Retell agent draft

Store versioned configuration

Outputs:

outputs/accounts/<account_id>/v1/account_memo.json
outputs/accounts/<account_id>/v1/agent_spec.json
Pipeline B — Onboarding → Agent v2

Input:

Onboarding transcript

Process:

Extract configuration updates

Patch the v1 account memo

Generate updated agent spec

Produce changelog

Outputs:

outputs/accounts/<account_id>/v2/account_memo.json
outputs/accounts/<account_id>/v2/agent_spec.json
outputs/accounts/<account_id>/v2/changes.md
Running the Pipeline

Run the batch pipeline:
python scripts/run_batch.py

This processes:

Demo → v1 agent
Onboarding → v2 agent
Generate changelog
n8n Workflow

Two automation workflows are included:

workflows/demo_to_v1.json
workflows/onboarding_to_v2.json

These workflows trigger the pipeline scripts and orchestrate the processing steps.

Zero Cost Implementation

This project uses only free tooling:

Python

Local file storage

n8n (local Docker deployment)

Open-source transcription tools

No paid APIs or services were used.

Known Limitations

CRM integrations are mocked (Jobber integration not available yet)

Emergency routing rules rely on transcript clarity

Audio transcription quality may affect extraction accuracy

Future Improvements

If deployed in production, the following improvements would be implemented:

Automated speech-to-text pipeline

Structured database storage (Supabase)

Direct Retell API agent creation

Web dashboard for account configuration

Automated QA validation of agent prompts

Demo

A short Loom walkthrough demonstrates:

Running the pipeline

Generated outputs

Version updates (v1 → v2)
