# Concepts

- Engines: selectable network stacks for different behaviors (resources/ScriptEnvironment.py:258–264).
- Injection markers: `%s` in `target.req`; payloads are substituted left-to-right (src/Request.kt:99–110).
- Queueing:
  - `engine.queue(template, payloads, learn, callback, gate, label, pauseBefore, pauseTime, pauseMarker, delay, endpoint, fixContentLength)` (src/RequestEngine.kt:93–131).
  - Per-request overrides like `endpoint` and `label`.
- Labels and state: record across responses via `req.label` and `engine.userState` (resources/examples/timingAttackWithState.py:8–23).
- Baseline learning: ignore boring responses using `learn=1/2/...` (src/RequestEngine.kt:371–401).
- Output: add interesting requests to the table with `table.add(req)`.