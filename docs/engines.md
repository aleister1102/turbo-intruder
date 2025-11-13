# Engines

- BURP (HTTP/1): uses Burp HTTP/1 stack; supports proxies; batches gated groups (src/BurpRequestEngine.kt:14–17, 111–176).
- BURP2 (HTTP/2): uses Burp HTTP/2 stack; enables single-packet sync via gating (src/BurpRequestEngine.kt:127–135).
- THREADED: custom TCP engine with fine-grained socket reads/writes, pauses, partial reads (src/ThreadedRequestEngine.kt:18–24).
- HTTP2: custom HTTP/2 engine with connection pool and retry logic (src/HTTP2RequestEngine.kt:16–37, 59–82).
- Limitations:
  - BURP/BURP2 disable pipelining and force one request per connection (resources/ScriptEnvironment.py:281–286).
  - `SPIKE` is experimental/unavailable in current build (src/SpikeEngine.kt).