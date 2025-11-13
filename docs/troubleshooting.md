# Troubleshooting

- Deadlock on gates:
  - Ensure gated request count ≤ `concurrentConnections` (src/RequestEngine.kt:142–145).
- Payload/marker mismatch:
  - `%s` present without payload or vice versa (src/RequestEngine.kt:99–106).
- Missing Content-Length:
  - THREADED may fall back to timed reads; set `applySetting("ignoreLength", true)` if needed (src/ThreadedRequestEngine.kt:430–459; src/RequestEngine.kt:428–434).
- Connection drops:
  - Requests re-queued up to retry cap; permanent failures counted (src/HTTP2RequestEngine.kt:63–76; src/RequestEngine.kt:404–426).
- Burp version compatibility:
  - Update Burp for `makeHttpRequest` and anomaly ranking (src/BurpRequestEngine.kt:73–76; src/RequestEngine.kt:322–334).