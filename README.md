# AI Agent Security Lab

## Purpose

This project is a clean-room security engineering lab focused on AI agent security, secure release engineering, and responsible AppSec analysis.

It studies a public source-map leakage incident involving an AI coding assistant ecosystem as a case study, without storing, copying, redistributing, or reproducing any leaked or proprietary source code.

The goal is to demonstrate how security teams can evaluate AI agent platforms, release artifacts, tool permission models, plugin ecosystems, and CI/CD controls in a professional and ethical way.

## Why AI Agent Security Matters

AI coding assistants and agentic developer tools increasingly interact with source repositories, terminals, package managers, cloud services, issue trackers, documents, and external tools. This creates new security questions for engineering and AppSec teams:

- What data can the agent access?
- Which tools can it invoke?
- How are sensitive actions approved?
- What artifacts are shipped to users?
- How are plugins, MCP servers, and third-party integrations reviewed?
- How are prompts, memory, logs, and context protected?

AI agent security is not only a model-safety topic. It is also release engineering, supply-chain security, access control, logging, governance, and incident response.

## What This Lab Covers

This repository covers practical AI agent security topics:

- AI agent threat modeling
- Source map and release artifact leakage risk
- Tool permission model security
- MCP and plugin supply-chain risk
- Prompt injection and excessive agency risk
- Context and memory exposure risk
- CI/CD controls to prevent accidental source disclosure
- Security checklists for npm and CLI package publishing
- OWASP LLM risk mapping

## Legal and Ethical Disclaimer

This project is for defensive security education and professional portfolio demonstration only.

This repository does not clone, fork, mirror, store, include, or redistribute leaked or proprietary source code. It does not reproduce proprietary code snippets. The case study material is written as a clean-room analysis using public reporting, official documentation, industry references, and general security engineering principles.

The key message is simple: this project is not about leaked code. It is about secure release engineering, AI agent security, and responsible AppSec analysis.

## Skills Demonstrated

- Application security analysis
- AI agent threat modeling
- Secure release engineering
- CI/CD security controls
- npm package review
- Software supply-chain risk assessment
- Source map exposure analysis
- OWASP LLM Top 10 mapping
- STRIDE threat modeling
- Incident response planning
- Security documentation for technical and non-technical reviewers

## Repository Structure

```text
ai-agent-security-lab/
  README.md
  docs/
    01-source-map-leakage-case-study.md
    02-ai-agent-threat-model.md
    03-tool-permission-security.md
    04-mcp-supply-chain-risk.md
    05-context-memory-risk.md
    06-release-pipeline-controls.md
  labs/
    lab-01-source-map-risk/
    lab-02-tool-permission-model/
    lab-03-prompt-injection/
    lab-04-mcp-risk-simulation/
  controls/
    release-checklist.md
    ci-cd-security-gates.md
    npm-package-review-checklist.md
    sbom-checklist.md
  threat-models/
    ai-agent-data-flow.md
    stride-ai-agent.md
    owasp-llm-mapping.md
```

## How Recruiters and Security Teams Can Review This Project

Start with the README to understand the scope and ethical boundary of the work.

Then review:

- `docs/01-source-map-leakage-case-study.md` for clean-room analysis of release artifact leakage risk.
- `controls/release-checklist.md` for practical release controls.
- `threat-models/stride-ai-agent.md` for structured AI agent threat modeling.
- `threat-models/owasp-llm-mapping.md` for alignment with OWASP LLM security categories.
- `labs/` for hands-on educational simulations that avoid proprietary material.

This repository is intended to show security judgment, documentation quality, and practical AppSec thinking rather than exploit development or code disclosure.

