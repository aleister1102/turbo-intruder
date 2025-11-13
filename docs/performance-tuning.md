# Performance Tuning

- Concurrency:
  - `concurrentConnections`, `requestsPerConnection`, `pipeline` grouping (resources/examples/default.py; src/ThreadedRequestEngine.kt).
- Socket tuning:
  - `readSize`, timeouts, `resumeSSL` reuse; `explodeOnEarlyRead` for strict timing (src/ThreadedRequestEngine.kt:18, 430–459, 546–567).
- Queue sizing:
  - `maxQueueSize`; auto-unlimit for non-streaming attacks (src/RequestEngine.kt:154–177).
- Retries:
  - Per-request retry cap and permanent failure counting (src/RequestEngine.kt:404–426; src/HTTP2RequestEngine.kt:63–76).
- RPS measurement:
  - Status string and summary (src/RequestEngine.kt:354–365, 271–292).