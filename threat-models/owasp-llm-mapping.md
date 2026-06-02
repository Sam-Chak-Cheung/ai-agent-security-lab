# OWASP LLM Mapping

## Purpose

This document maps the AI Agent Security Lab topics to the OWASP Top 10 for Large Language Model Applications. It is designed for portfolio review and AppSec discussion, not exploit development.

The mapping is clean-room and defensive. It uses generic AI agent scenarios and does not include leaked or proprietary source code.

## Mapping Summary

| OWASP LLM Risk Area | AI Agent Scenario | Security Impact | Controls Demonstrated in This Repo |
| --- | --- | --- | --- |
| Prompt Injection | Repository file or external webpage instructs the agent to ignore user intent | Unauthorized tool use, data disclosure, unsafe code change | Prompt-injection lab, context isolation, instruction hierarchy |
| Sensitive Information Disclosure | Agent includes secrets, source, or private context in logs or external calls | Credential exposure, privacy breach, source disclosure | Secret scanning, redaction, context minimization |
| Supply Chain | MCP server, plugin, npm dependency, or package script behaves maliciously | Tool compromise, dependency compromise, unauthorized actions | MCP risk docs, package review, SBOM checklist |
| Data and Model Poisoning | Retrieved documents or project files contain misleading security guidance | Incorrect recommendations, unsafe generated changes | Source validation, provenance checks, review gates |
| Improper Output Handling | Generated output is executed or published without validation | Vulnerable code, unsafe configs, bad release artifacts | Human review, tests, artifact inspection |
| Excessive Agency | Agent has broad filesystem, shell, network, or release permissions | High-impact unintended actions | Tool permission model, approval gates, least privilege |
| System Prompt Leakage | Agent reveals internal policies, guardrails, or hidden instructions | Bypass assistance, policy exposure | Separate policy from user context, do not rely on secrecy |
| Vector and Embedding Weaknesses | RAG content retrieval includes untrusted or poisoned text | Prompt injection or misleading context | RAG provenance and trust-boundary review |
| Misinformation | Agent produces confident but incorrect security conclusions | Poor decisions, missed controls | Reviewer notes, evidence-based impact analysis |
| Unbounded Consumption | Agent loops through costly tools or CI tasks | Denial of service, cost increase | Rate limits, timeouts, quotas, cancellation |

## Detailed Control Mapping

### Prompt Injection

| Review Question | Expected Control |
| --- | --- |
| Can repository text override system or developer instructions? | Treat repository content as untrusted data |
| Can external webpages influence tool use? | Require approval before sensitive actions |
| Are instructions separated by trust level? | Keep system policy, user prompts, and retrieved content distinct |
| Is prompt injection tested safely? | Use synthetic examples only |

### Sensitive Information Disclosure

| Review Question | Expected Control |
| --- | --- |
| Can secrets enter the model context? | Run secret scanning and redact sensitive values |
| Are logs safe for support and audit users? | Apply log redaction and access controls |
| Can source maps expose original source? | Exclude unintended `.map` files and inspect artifacts |
| Is package content reviewed before publishing? | Use package allowlists and release approval |

### Supply Chain

| Review Question | Expected Control |
| --- | --- |
| Are MCP servers and plugins reviewed before use? | Verify publisher, permissions, endpoint, and behavior |
| Are npm dependencies reviewed? | Use lockfiles, SBOMs, vulnerability checks, and package provenance |
| Can install scripts modify the workspace? | Disable or isolate lifecycle scripts where practical |
| Are release artifacts reproducible? | Preserve build logs, hashes, and SBOM evidence |

### Data and Model Poisoning

| Review Question | Expected Control |
| --- | --- |
| Can retrieved content affect security recommendations? | Track source provenance and prefer authoritative references |
| Are stale or malicious docs detected? | Review source age, ownership, and trust level |
| Can untrusted examples become production code? | Require tests, review, and policy checks |

### Improper Output Handling

| Review Question | Expected Control |
| --- | --- |
| Is generated code executed automatically? | Require review for generated code and commands |
| Are generated CI changes reviewed? | Protect workflow files and release scripts |
| Are generated release artifacts inspected? | Review tarballs, bundles, source maps, and metadata |

### Excessive Agency

| Review Question | Expected Control |
| --- | --- |
| Can the agent publish packages, push code, or deploy? | Require explicit approval and least-privilege tokens |
| Can it delete or overwrite files broadly? | Enforce path scoping and sensitive-command gates |
| Can it install arbitrary tools? | Require dependency review and sandboxing |

## Crosswalk to Repository Files

| Repository File | OWASP Topics Supported |
| --- | --- |
| `docs/01-source-map-leakage-case-study.md` | Sensitive Information Disclosure, Improper Output Handling |
| `docs/03-tool-permission-security.md` | Excessive Agency, Prompt Injection |
| `docs/04-mcp-supply-chain-risk.md` | Supply Chain, Sensitive Information Disclosure |
| `docs/05-context-memory-risk.md` | Sensitive Information Disclosure, Prompt Injection |
| `controls/release-checklist.md` | Improper Output Handling, Supply Chain |
| `controls/npm-package-review-checklist.md` | Supply Chain, Sensitive Information Disclosure |
| `labs/lab-02-tool-permission-model/README.md` | Excessive Agency |
| `labs/lab-03-prompt-injection/README.md` | Prompt Injection |

## Reviewer Notes

This mapping shows that AI agent security is broader than prompt safety. A recruiter or security reviewer should see coverage across:

- AppSec threat modeling
- Software supply-chain controls
- Secure release engineering
- Permission and approval design
- Context and data handling
- Incident prevention and response

The repo intentionally avoids unsafe reproduction of real incident artifacts. It focuses on what a security engineer should learn and how controls can be designed.

