# HTTP/2 Notes

- Header rewrites in HTTP/2 engines:
  - `^` → `\r`, `~` → `\n`, `` ` `` → `:` (resources/examples/http2.py:8–14).
  - Override pseudo-headers by specifying them like normal headers.
- Single-packet attack:
  - Use BURP2 and a gate to synchronize frames (resources/examples/race-single-packet-attack.py:3–9; src/BurpRequestEngine.kt:127–135).
- Streams and frames:
  - Lifecycle and response assembly (src/Stream.kt:27–106).
- Connection management and retries:
  - Pool replacement and re-queueing behavior (src/HTTP2RequestEngine.kt:39–82).