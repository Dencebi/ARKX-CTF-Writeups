# Level 9 — Blind Network Ninja

**Status:** Passed.

## Solution summary

The successful input used shell command chaining and command substitution to read the challenge's local flag file and make a request to the local HTTP service using that value as the request path.

## Observed output

The challenge logs showed a request path containing the generated flag, for example:

```text
GET /flag-2f609d
```

Submitting `flag-2f609d` was accepted in that run.

## Important: flags can change between runs

An earlier run produced `flag-29a5dc`; the successful run recorded here produced `flag-2f609d`. Treat these as run-specific evidence, not universal answers. Check the current run's logs and submit the value observed there.

## Security lesson

This challenge demonstrates the risk of passing untrusted input to a shell. In real systems, avoid shell interpretation of user-controlled strings; use safe process APIs and strict input validation.

## Evidence limitations

The successful input was recorded in the conversation, but the exact accepted flag may be session-specific. The values above document the observed run only.