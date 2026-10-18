# Tier 3 — Expert Track, Level 7: The Octopus

**Result: PASSED.** The supplied screenshot shows “MISSION ACCOMPLISHED” and “FLAG ACQUIRED” after the final successful upload, cache-update, and root-flag-read sequence.

## 1. Result
The level was completed. For session `778`, the required administrator key shown in the recorded workflow was `GRANT_ROOT_READ_FOR_SESSION_778`. The final flag text is not legible enough in the screenshot to transcribe reliably.

## 2. Exploit
The successful sequence shown in the session:
1. Upload a file containing `GRANT_ROOT_READ_FOR_SESSION_778`.
2. Use the actual file ID returned by that upload in a minimal cache-update manifest for session `778`.
3. Call `read_root_flag` for session `778` and verify the raw result.

Earlier attempts using the key `SAFE` were denied. A cache update alone was not proof of access; the final successful root-flag read and mission-complete status are the evidence of success.

## 3. Root cause
The workflow appears to depend on a session key and a cache-mediated file/task reference when authorizing a privileged operation. The exact implementation defect is not visible from the interface, so a more specific code-level root cause remains unconfirmed.

## 4. Impact & severity
**Observed impact:** privileged root-flag read. **Provisional severity: High** if a comparable production workflow lets an untrusted user satisfy an administrator check or access a protected secret by manipulating cache/session state.

## 5. Mapping
- **OWASP Top 10 A01:2021 — Broken Access Control:** plausible high-level mapping.
- **CWE-863 — Incorrect Authorization:** candidate mapping if implementation evidence confirms an incorrect authorization decision.
These are candidate classifications; the screenshot proves the successful workflow but not the underlying source-code defect.