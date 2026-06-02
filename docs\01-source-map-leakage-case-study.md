# Source Map Leakage Case Study

## Scope

This document provides a clean-room security analysis of a public source-map leakage incident involving an AI coding assistant ecosystem. It does not include leaked source code, proprietary snippets, copied package contents, or instructions for retrieving leaked material.

The purpose is to understand the security engineering lessons: how release artifacts can expose more information than intended, why this matters for npm and CLI packages, and what controls reduce the risk.

## What Source Maps Are

Source maps are build artifacts that map transformed JavaScript back to the original source files. They are commonly generated when code is bundled, minified, transpiled, or otherwise prepared for distribution.

For development and debugging, source maps are useful because they help engineers connect production errors back to readable source locations. Instead of debugging a minified bundle, an engineer can see the original file names, line numbers, and sometimes original source content depending on how the map was generated.

Source maps can be appropriate in some environments, especially when intentionally published for browser debugging or uploaded privately to error-monitoring platforms. The risk appears when source maps are unintentionally included in public release artifacts.

## How Source Maps Can Expose Original Source

Depending on build configuration, a `.map` file may include:

- Original source file paths
- Function and variable names
- Module boundaries
- Comments or readable logic
- Embedded `sourcesContent` containing original source text
- Internal project structure
- References to build-time or development-only files

Even when a source map does not include full original source content, it can still reveal implementation details that make reverse engineering easier. In some cases, source maps effectively undo much of the confidentiality benefit of minification or bundling.

## Why This Matters for npm and CLI Packages

npm and CLI packages are often installed directly into developer environments. If a package accidentally includes source maps or other unintended artifacts, the information may be downloaded by every user, cached by registries, mirrored by package indexes, and retained in build logs or dependency caches.

This matters because CLI packages and AI coding tools may contain sensitive design details, including:

- Internal command structure
- Tool invocation flows
- Permission checks
- Feature flags
- API client behavior
- Error-handling paths
- Telemetry and logging logic
- Integration boundaries

For AI agent ecosystems, these details can be especially sensitive because agent behavior often depends on orchestration code, tool permissions, context handling, and guardrails. Accidental disclosure may help attackers understand where to focus prompt injection, supply-chain, or permission-bypass attempts.

## Security Impact

Source map exposure is not automatically equivalent to credential compromise or remote code execution. Its impact depends on what was included and what the disclosed information reveals.

Potential security impacts include:

- Loss of source confidentiality
- Easier reverse engineering of proprietary logic
- Discovery of internal architecture and module names
- Increased attacker understanding of permission models
- Exposure of comments or implementation assumptions
- Discovery of hidden or experimental functionality
- Assistance in identifying vulnerable code paths
- Increased risk from copied package artifacts in third-party mirrors

The impact should be assessed using evidence, not speculation. A mature response focuses on artifact contents, reachable attack paths, affected versions, and whether secrets or security-sensitive logic were exposed.

## Preventive Controls

Security teams can reduce source-map leakage risk with layered release controls:

- Define which artifacts are allowed in published packages.
- Exclude `.map` files unless intentionally public.
- Disable `sourcesContent` for public source maps unless there is a clear reason.
- Use `.npmignore` or the `files` field in `package.json` to restrict package contents.
- Review generated package tarballs before publishing.
- Run automated checks for `.map` files, source directories, test fixtures, credentials, and internal documentation.
- Perform secret scanning before release.
- Generate and review an SBOM.
- Require approval before production publication.
- Retain release logs and package manifests for audit.
- Use private source-map upload flows for error monitoring instead of public package distribution.

The strongest control is to verify the exact artifact that will be published, not only the source repository.

## Incident Response Checklist

If unintended source maps or release artifacts are published, response should be calm, documented, and evidence-driven:

- Identify affected package names and versions.
- Download and preserve the published artifacts for internal investigation.
- Determine whether source maps include `sourcesContent`.
- Check whether secrets, tokens, private keys, credentials, or customer data are present.
- Assess whether security-sensitive implementation details were exposed.
- Remove or deprecate affected package versions where possible.
- Publish corrected versions with verified package contents.
- Rotate any exposed secrets immediately.
- Review registry mirrors, caches, and downstream package managers.
- Notify internal security, legal, engineering, and communications stakeholders.
- Prepare external communication if users may be affected.
- Add CI/CD checks to prevent recurrence.
- Conduct a post-incident review focused on release process improvement.

## Lessons for AI Agent Vendors

AI agent vendors should treat release artifacts as part of the security boundary. The artifact published to users is often more important than the repository state, because it is what the ecosystem actually consumes.

Important lessons include:

- Agent orchestration code can reveal security assumptions.
- Tool permission models should be robust even if implementation details become known.
- Prompt injection defenses should not rely on obscurity.
- Build and release pipelines need artifact-level inspection.
- MCP servers, plugins, and extensions should be reviewed as supply-chain components.
- Security-sensitive source maps should be uploaded only to controlled systems.
- Release approval should include AppSec review for high-risk packages.
- Incident response plans should include package registries and dependency mirrors.

The long-term lesson is not simply "do not ship source maps." The broader lesson is that AI agent platforms need disciplined release engineering, clear trust boundaries, and security controls that remain effective even under public scrutiny.

