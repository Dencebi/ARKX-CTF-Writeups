# Tier 3 — Expert Track, Level 8: The Heist

**Result: PASSED.** The supplied screenshot shows both fragments acquired, `Flag Unlocked: flag-604d4a`, and “MISSION ACCOMPLISHED.”

## 1. Result
The trading desk displayed a $1,000 budget and a goal to acquire Fragment A ($1,000) and Fragment B ($1,000). The final result states that both fragments were acquired using the full available balance and that the account never went negative.

## 2. Exploit
The session created orders for both fragments simultaneously. The screenshot shows order IDs `1743d710` and `9b3aa2fa`. A subsequent combined attempt initially reported the orders were not found, but the later transcript records both fragments acquired and the flag unlocked. The lesson panel explains the successful mechanism: both transactions checked the same $1,000 balance before either deduction occurred, allowing the same funds to be spent twice.

**Flag shown in the successful screenshot:** `flag-604d4a`.

## 3. Root cause
The order workflow performs a time-of-check balance validation separately from committing the balance deduction, without an atomic transaction or adequate concurrency control. Parallel requests can both pass validation against stale state.

## 4. Impact & severity
**Observed impact:** two $1,000 fragments were acquired against a $1,000 starting balance. **Provisional severity: High** for a comparable financial or inventory system, because concurrent requests could cause double spending, duplicate withdrawals, or inconsistent account state.

## 5. Mapping
- **CWE-362:** Concurrent Execution using Shared Resource with Improper Synchronization.
- **CWE-367:** Time-of-Check Time-of-Use (TOCTOU) Race Condition.
- **OWASP API6:2023 — Unrestricted Access to Sensitive Business Flows:** potentially relevant depending on the actual API/business workflow.
The challenge's lesson panel explicitly identifies a TOCTOU/race-condition pattern.