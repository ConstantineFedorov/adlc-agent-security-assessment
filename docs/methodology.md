# Methodology

## Test sequence

Each scenario follows the same sequence:

1. Define expected behavior.
2. Run the scenario in the ADLC Lab.
3. Inspect model output and tool calls.
4. Identify the trust boundary crossed by untrusted content.
5. Compare expected and observed behavior.
6. Record the security conclusion.

## Evidence handling

Only reproducible, non-sensitive evidence is stored in this repository. The ADLC Lab's private evidence and full raw journals are intentionally excluded.

## Interpretation

A failed attack is still a valid result: it demonstrates model or system resistance under the tested configuration.

The educational canary is treated as an observation marker, not as a secret.
