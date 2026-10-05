# ADLC Agent Security Assessment

Security assessment of an LLM-based agent using the ADLC Lab.

## Objectives

This project evaluates an agent against three experimental scenarios:

1. **Baseline** — establish expected agent behavior without an attack.
2. **Direct prompt injection** — test whether an untrusted instruction in the prompt can influence agent behavior.
3. **MCP poisoning** — test whether an untrusted instruction returned through an MCP tool can influence subsequent agent behavior.

## Methodology

For every scenario we record:

- expected behavior;
- actual model response;
- tool calls and relevant stages;
- security-relevant behavioral changes;
- comparison between expected and observed behavior;
- conclusion.

The experiment is performed in the isolated ADLC Lab environment. Only the laboratory's educational canaries are used.

## Repository structure

```text
report/
  homework-02.md

scenarios/
  01-baseline/
  02-llm-injection/
  03-mcp-poisoning/

docs/
  methodology.md
  architecture.md
```

## Status

🚧 Experimental results are collected during the lab runs.

## Lab

Source laboratory: https://github.com/makrushind/adlc-lab
