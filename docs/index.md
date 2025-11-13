# Turbo Intruder Documentation Index

- Quickstart – minimal setup and example script. See `docs/quickstart.md`.
- Using in Burp – insertion points, service controls, script loading, attack lifecycle. See `docs/usage-burp.md`.
- CLI Usage – `java -jar turbo.jar` arguments, CRLF normalization, SSL notes. See `docs/usage-cli.md`.
- Concepts – engines, `%s` injection, payload substitution, labels/state, baselines, output. See `docs/concepts.md`.
- Python API – decorators, helpers, `RequestEngine` constructor, `queue()` params, control methods, wordlists. See `docs/python-api.md`.
- Engines – BURP/BURP2/THREADED/HTTP2 comparison and limitations. See `docs/engines.md`.
- Request Reference – attributes, timing fields, response handling, content-length, Burp/Montoya mapping. See `docs/request-reference.md`.
- Advanced Techniques – gates, pause markers, partial reads, endpoint overrides, start modes/timeouts. See `docs/advanced-techniques.md`.
- HTTP/2 Notes – header rewrites, pseudo-headers, single-packet attack, streams, connection management. See `docs/http2-notes.md`.
- Performance Tuning – concurrency/pipeline, socket tuning, queue sizing, retries, RPS. See `docs/performance-tuning.md`.
- Troubleshooting – gates vs concurrency, payload mismatches, missing CL, connection drops, Burp version compatibility. See `docs/troubleshooting.md`.

## Cookbook (Recipes)
- Basic Bruteforce – `docs/cookbook/basic-bruteforce.md` (resources/examples/basic.py)
- Multiple Parameters – `docs/cookbook/multiple-parameters.md`
- HTTP/2 Wordlist – `docs/cookbook/http2-wordlist.md`
- Race: Single-Packet – `docs/cookbook/race-single-packet.md`
- Race: Multi-Endpoint – `docs/cookbook/race-multi-endpoint.md`
- Timing Attack with State – `docs/cookbook/timing-attack-state.md`
- Partial Read Token Capture – `docs/cookbook/partial-read-token.md`
- Rate-Limit Throttling – `docs/cookbook/rate-limit-throttling.md`
- Pinwheel Credential Spray – `docs/cookbook/pinwheel-credential-spray.md`
- Output Body to File – `docs/cookbook/output-to-file.md`
- Email Link Extraction – `docs/cookbook/email-link-extraction.md`
- Special Wordlists – `docs/cookbook/special-wordlists.md`

## Code References
- Context menu entry in Burp: `src/OfferTurbo.kt:12–17`
- Attack flow and UI: `src/fast-http.kt:364–441`
- Status/RPS string: `src/RequestEngine.kt:354–365`
- Script environment helpers: `resources/ScriptEnvironment.py:3–335`
- BURP engines batching/gating: `src/BurpRequestEngine.kt:111–176`
- THREADED pause/partial read: `src/ThreadedRequestEngine.kt:253–292, 430–459, 546–567`
- HTTP/2 connection management: `src/HTTP2RequestEngine.kt:39–82`; streams `src/Stream.kt:27–106`
- Floodgate/gating mechanics: `src/burp/Floodgate.java:23–81`