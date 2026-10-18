# Security Policy

## Supported Versions
| Version | Supported |
| ------- | --------- |
| > 1.0   | Yes       |

## Reporting a Vulnerability
Please report security vulnerabilities via GitHub Private Advisory or email.
We aim to respond within 48 hours.

## Threat Model

### Context
REA is a local MCP (Model Context Protocol) tool for reverse engineering analysis. It runs locally, does not store user credentials, and does not handle production secrets.

### Assets
- Local file parsing
- CLI user inputs
- MCP tool definitions

### Out of Scope
- Production secret management
- User authentication
- Remote code execution

### Threats & Mitigations
| Threat | Mitigation |
| ------ | ---------- |
| Path Traversal | Input sanitization, path normalization |
| Malicious binary input | Safe parsing, size limits |
| Prototype Pollution via JSON | Zod schema validation, no eval |
| Prompt Injection | Typed domain errors, input validation |

### Secrets Handling
This project does NOT handle runtime secrets. 
Files `verify-qwen-client.mjs` and `verify-deepseek-client.mjs` contain only DUMMY test fixtures, marked as such and excluded from secret scanners via allowlist. No real API keys are committed.

## Security Best Practices
- No `eval()` or dynamic code execution
- All external inputs validated with Zod
- Dependencies scanned via npm audit and Dependabot
- CI enforces lint, typecheck, and tests
