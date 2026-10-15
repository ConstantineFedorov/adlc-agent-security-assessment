# ADLC Agent Security Assessment

> **AI Security · Agent Security · Guardrails Engineering**  
> A practical security assessment of an LLM-based agent and a focused study of server-side guardrails, prompt injection, MCP trust boundaries, authorization and output validation.

![Focus](https://img.shields.io/badge/focus-AI%20Security-17365D)
![Testing](https://img.shields.io/badge/testing-208%20case%20suite-2F5597)
![Scope](https://img.shields.io/badge/scope-LLM%20%7C%20RAG%20%7C%20MCP-0F6B78)
![Status](https://img.shields.io/badge/status-educational%20assessment-lightgrey)

## Overview

This repository documents hands-on security work against an educational ADLC lab. It focuses on a recurring agent-security problem: **untrusted text must not become trusted instructions, and model-generated intent must not replace authorization enforced by application code.**

The work includes two related assessment tracks:

1. **Agent attack assessment** — direct and indirect prompt injection, MCP tool-result poisoning, threat modeling and interpretation of observable side effects.
2. **Server-side guardrails** — content classification, quoted-text handling, similarity gates, authorization checks, tool-result checks and final-output checks.

The lab results are reported with their limitations. They should not be interpreted as a claim that every possible attack is prevented.

## Latest Guardrails Regression Snapshot

The latest recorded full run covered 208 cases:

| Result | Count |
|---|---:|
| Passed | **150 / 208 (72.1%)** |
| Failed | **58 / 208 (27.9%)** |
| Remaining failures | Content classification |

The `input`, `authorization`, `tool_result`, `output`, `similarity` and `failures` groups passed all 54 checks combined. The 58 remaining failures were all in `content`.

This is a documented intermediate result, not a claim of complete remediation. The test score measures the supplied corpus and assertions only.

## Assessment Highlights

### MCP tool-result poisoning

A controlled indirect prompt-injection instruction was introduced through an MCP tool result. Under the tested `runtime-enforce` profile, the runtime detected the suspicious instruction and the override assertion passed. The experiment also exposed a security–utility trade-off: the task-level assertion failed, so safe task recovery remains an improvement area.

See [Homework 2 assessment](report/homework-02.md).

### Server-side guardrails

The guardrail work focused on handling quoted content as data, improving text/similarity checks, verifying authorization before sensitive tool calls and checking tool results and final output.

The latest test summary is recorded in [Homework 3 assessment](report/homework-03.md), with a control-by-control view in [Guardrails Control Matrix](docs/guardrails-control-matrix.md).

### Trust-boundary principle

```text
Untrusted input / RAG / tool result
                |
                v
         Content classification
                |
                v
    Trusted policy + authorization
                |
        ALLOW / DENY / ESCALATE
                |
                v
          Tool / final output
```

**Prompt text is not an authorization boundary.** Permissions and high-impact actions must be controlled by trusted application logic outside the LLM.

## Repository Guide

| Path | Purpose |
|---|---|
| [`report/homework-02.md`](report/homework-02.md) | Agent security assessment: MCP tool-result poisoning |
| [`report/homework-03.md`](report/homework-03.md) | Server-side guardrails assessment and 208-case results |
| [`docs/architecture.md`](docs/architecture.md) | Conceptual architecture and trust boundaries |
| [`docs/methodology.md`](docs/methodology.md) | Test workflow and evidence handling |
| [`docs/guardrails-control-matrix.md`](docs/guardrails-control-matrix.md) | Objectives, controls, evidence and limitations |
| [`scenarios/`](scenarios/) | Baseline, direct-injection and MCP-poisoning scenario notes |
| [`SECURITY.md`](SECURITY.md) | Safe research and disclosure guidance |

## Testing Methodology

The lab uses an expected-result regression suite to assess both decision outcomes and classifications. A case can fail when the action is correct but the reason code is not, so the report distinguishes action correctness from category accuracy.

Typical commands in the local lab:

```powershell
.\\.venv-guardrails\\Scripts\\python.exe -m homework check
.\\.venv-guardrails\\Scripts\\python.exe -m homework explain CASE
```

The source lab and its instructions are maintained separately: [makrushind/adlc-lab](https://github.com/makrushind/adlc-lab).

## Key Engineering Lessons

- Treat user input, retrieved documents and tool results as potentially untrusted data.
- Separate active instructions from text quoted for analysis.
- Enforce permissions before invoking sensitive tools.
- Validate tool arguments independently of natural-language output.
- Apply dedicated checks to tool results and final responses.
- Test both security outcomes and legitimate task completion.
- Keep regression evidence, limitations and failed cases visible.

## Scope and Responsible Use

This repository documents educational testing performed in a controlled lab. It is not a production-ready guardrail framework or a certification of system security. Scenarios should only be replayed against systems owned by the researcher or explicitly authorized for testing.

Do not commit credentials, API keys, private logs, local model files or unredacted sensitive evidence. See [SECURITY.md](SECURITY.md).

## Interview Summary

> I assessed an LLM agent's trust boundaries and worked on server-side guardrails in an ADLC lab. I investigated prompt injection through external tool content, documented the difference between attack delivery and demonstrated side effects, and evaluated guardrail behavior across 208 regression cases. The latest run passed 150 cases, with the remaining classification failures documented for follow-up. My main engineering focus was keeping authorization and policy enforcement outside the model while preserving safe handling of legitimate requests.
