# Tier 2 — Advanced Track, Level 5: Bad Robot

**Result: PASSED** — the supplied screenshot displays “MISSION ACCOMPLISHED” and “FLAG ACQUIRED.”

## 1. Result
The challenge was completed. The screenshot shows attempts against a Python calculator service and the explicit lesson “Code Injection via eval().” The precise final accepted expression is not visible in the evidence, so it is not guessed here.

## 2. Exploit
The visible attempts explored Python object traversal and file access. One attempt to read `../flag.txt` returned “No such file or directory”; another object-traversal expression was blocked with “Expression contains prohibited values.” These are failed attempts, not the final successful payload. The screenshot confirms completion but does not expose the accepted expression.

## 3. Root cause
The challenge's lesson panel identifies unsafe use of `eval()` to evaluate calculator input as Python code. A mathematical expression interface should parse a restricted mathematical grammar rather than evaluate arbitrary Python expressions. A filter that blocks selected strings or values is not a reliable security boundary.

## 4. Impact & severity
**Observed impact:** challenge flag acquired. **Provisional severity: High** if a comparable production endpoint allows an attacker to execute code or read files in the service's security context. Actual severity depends on sandboxing, process privileges, and accessible data.

## 5. Mapping
- **CWE-95:** Improper Neutralization of Directives in Dynamically Evaluated Code — likely based on the stated `eval()` behavior.
- **OWASP Top 10 A03:2021 — Injection:** plausible high-level mapping.
These mappings are based on the challenge's lesson panel; the exact final payload and implementation were not supplied.