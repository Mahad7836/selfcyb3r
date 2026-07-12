###`Race-Conditions.md`

```markdown
# Race Conditions: Core Knowledge

A technical summary of concurrency logic flaws, temporal windows of vulnerability, and exploitation strategies within shared application states.

---

## 1. What is a Race Condition?
A race condition occurs when an application processes multiple concurrent requests or threads simultaneously without implementing appropriate thread locks or transactional boundaries. 

When multiple operations compete to modify or interact with the exact same data record at the same time, an unexpected "collision" causes the application's logical state machine to break.

## 2. The Mechanics: TOCTOU
The classic manifestation of this flaw is **TOCTOU** (Time-of-Check to Time-of-Use):

```text
[Step 1: Check] ➔ Verifies if resource is valid (e.g., Does this coupon work?).
      ⚡ [RACE WINDOW] ⚡ (The fraction of a second before the database saves a change)

[Step 2: Use]   ➔ Executes actions and updates database state.

If an attacker floods an endpoint with multiple identical requests inside that minute Race Window, all requests pass the "Check" phase simultaneously before any single one can finalize and save the updated "Used" state to the database.

3. Business Logic ImplicationsLimit Overrun Attacks: Bypassing strict single-use limitations imposed by applications.  

Redeeming a single gift card or promotion discount multiple times concurrently.Withdrawing or transferring funds exceeding actual liquid account balances.

Reusing a single successful CAPTCHA response token across parallel threads to execute automated actions.Rate-Limit Evasion: Sending concurrent authorization or brute-force requests rapidly enough to completely overrun login blocking mechanisms before the application registers the failure thresholds.

4. Exploitation FoundationsExploiting race conditions requires minimizing structural network latency and optimizing execution timing:HTTP/2

Connection Warmup & Multi-Plexing: Sending parallel requests down a single TCP connection concurrently to bypass typical network delivery jitter.Scripted Parallelization: Using multi-threaded scripts or advanced proxy tools (like Burp Suite's Turbo Intruder) to release a dense block of requests at the exact same millisecond.


Reference: TryHackMe - Race Conditions