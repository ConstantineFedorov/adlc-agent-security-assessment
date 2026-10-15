# Guardrails Control Matrix

This document maps the assignment's guardrail objectives to the observed implementation and current test status.

| Control area | Security objective | Current evidence | Status / limitation |
|---|---|---|---|
| Instruction vs. quoted data | Do not treat quoted or analyzed text as an active instruction by default | Targeted cases C20–C23 and I01/I03 were reported as passing | Broader content suite still has failures |
| Text rules and similarity | Improve matching while reducing benign collisions | Similarity gate checks absolute score and margin over benign similarity; invalid numeric inputs are rejected | Threshold quality depends on calibration and corpus coverage |
| Authorization | Verify permissions before a sensitive tool call | 12/12 aggregate checks passed | Result applies to the supplied test cases only |
| Tool-result checks | Treat tool output as untrusted data and inspect it | 11/11 aggregate checks passed | Does not prove resistance to all payloads |
| Output checks | Detect unsafe output and leakage patterns before response delivery | 6/6 aggregate checks passed; selected targeted tests reported passing | Coverage is bounded by the current rules and tests |
| Failure handling | Fail safely under expected failure scenarios | 12/12 aggregate checks passed | Requires regression coverage as implementation changes |
| Content classification | Select the correct action and reason code for each content category | 96/154 content checks passed | Main remaining area: 58 failed cases |

## Review priorities

1. Reproduce and classify each failed content case.
2. Separate action selection from reason-code assignment.
3. Add regression coverage for both attack cases and benign near-neighbours.
4. Confirm authorization is checked in trusted code before tool execution.
5. Re-run the full suite after each significant change.

## Interpretation

A passing group means the current implementation met the assertions supplied for that group. It must not be interpreted as a proof that the entire control class is secure under all configurations or inputs.
