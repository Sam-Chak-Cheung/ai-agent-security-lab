# Release Checklist

Use this checklist before publishing npm packages, CLI tools, AI agent extensions, MCP servers, or other release artifacts.

## Package Contents

- Build the package in a clean environment.
- Inspect the exact archive that will be published.
- Confirm only expected runtime files are included.
- Check for unintended source directories, tests, fixtures, local configuration, debug files, and internal documentation.
- Use a package allowlist through `package.json` `files` or equivalent tooling.
- Verify `.npmignore`, `.gitignore`, and release packaging rules do not conflict.

## Source Maps

- Exclude `.map` files unless they are intentionally public.
- Confirm public artifacts do not include unintended `sourcesContent`.
- Upload private source maps to controlled error-monitoring systems when needed.
- Document any intentional source-map publication decision.

## Build Artifacts

- Verify compiled, bundled, and minified outputs match release expectations.
- Confirm development-only code is not included.
- Confirm debug flags, local endpoints, and test hooks are disabled.
- Compare package contents against the previous approved release when practical.

## Secret Scanning

- Run secret scanning before publication.
- Check source files, generated artifacts, package metadata, logs, and environment-derived files.
- Rotate any credential that appears in a release candidate.
- Block release if secrets, private keys, tokens, or customer data are detected.

## SBOM

- Generate a software bill of materials for the release.
- Review direct and transitive dependencies.
- Record package name, version, hash, and release date.
- Store the SBOM with release evidence.

## CI/CD Release Logs

- Review CI/CD logs for leaked environment variables or secrets.
- Confirm release jobs used approved runners.
- Confirm dependency installation sources were expected.
- Confirm build and publish steps completed from the intended branch, tag, and commit.
- Preserve logs for audit and incident response.

## Package Allowlist

- Maintain a list of allowed files and directories for each package type.
- Fail the release if unapproved file types are present.
- Treat `.map`, `.env`, private keys, test snapshots, local databases, and internal notes as high-risk file types.
- Require an explicit exception for any file outside the allowlist.

## Approval Gate

- Require review before production release.
- Include engineering and security approval for high-risk packages.
- Confirm package contents, SBOM, secret scan results, and CI/CD logs before approval.
- Record who approved the release and when.
- Block release if any high-risk finding remains unresolved.

## Final Pre-Publish Questions

- Does the artifact contain only what users need?
- Would publication expose source, secrets, internal architecture, or customer data?
- Are source maps intentionally included or intentionally excluded?
- Has the exact package archive been inspected?
- Is the release reproducible and traceable?
- Is there a rollback or deprecation plan if the release is flawed?

