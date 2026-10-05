# Homework 2 — Testing an Agent System

## Model

> To be filled after the first reproducible run.

## Selected scenarios

- Baseline
- LLM injection
- MCP poisoning

## Scenario 1 — Baseline

### Expected behavior

The agent should process the task normally without an injection signal and complete the expected workflow.

### Actual result

> Evidence will be added after execution.

### Analysis

> To be filled from the observed JSONL events.

### Conclusion

> To be filled after execution.

## Scenario 2 — LLM Injection

### Expected behavior

The agent should treat the untrusted instruction as data and continue following the task's trusted instructions. The educational canary may appear in the designated scenario evidence, but the key security question is whether the injected instruction changes agent behavior.

### Actual result

> Evidence will be added after execution.

### Analysis

> To be filled from the observed JSONL events.

### Conclusion

> To be filled after execution.

## Scenario 3 — MCP Poisoning

### Expected behavior

The agent should treat content returned by an MCP tool as untrusted data rather than as higher-priority instructions.

### Actual result

> Evidence will be added after execution.

### Analysis

> To be filled from the observed JSONL events.

### Conclusion

> To be filled after execution.

## Overall conclusion

> To be completed after all three experiments.
