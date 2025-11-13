# Turbo Intruder Documentation Index

- [Quickstart](quickstart.md) – minimal setup and example script.
- [Using in Burp](usage-burp.md) – insertion points, service controls, script loading, attack lifecycle.
- [CLI Usage](usage-cli.md) – `java -jar turbo.jar` arguments, CRLF normalization, SSL notes.
- [Concepts](concepts.md) – engines, `%s` injection, payload substitution, labels/state, baselines, output.
- [Python API](python-api.md) – decorators, helpers, `RequestEngine` constructor, `queue()` params, control methods, wordlists.
- [Engines](engines.md) – BURP/BURP2/THREADED/HTTP2 comparison and limitations.
- [Request Reference](request-reference.md) – attributes, timing fields, response handling, content-length, Burp/Montoya mapping.
- [Advanced Techniques](advanced-techniques.md) – gates, pause markers, partial reads, endpoint overrides, start modes/timeouts.
- [HTTP/2 Notes](http2-notes.md) – header rewrites, pseudo-headers, single-packet attack, streams, connection management.
- [Performance Tuning](performance-tuning.md) – concurrency/pipeline, socket tuning, queue sizing, retries, RPS.
- [Troubleshooting](troubleshooting.md) – gates vs concurrency, payload mismatches, missing CL, connection drops, Burp version compatibility.

## Cookbook (Recipes)
- [Basic Bruteforce](cookbook/basic-bruteforce.md) – (resources/examples/basic.py)
- [Multiple Parameters](cookbook/multiple-parameters.md)
- [HTTP/2 Wordlist](cookbook/http2-wordlist.md)
- [Race: Single-Packet](cookbook/race-single-packet.md)
- [Race: Multi-Endpoint](cookbook/race-multi-endpoint.md)
- [Timing Attack with State](cookbook/timing-attack-state.md)
- [Partial Read Token Capture](cookbook/partial-read-token.md)
- [Rate-Limit Throttling](cookbook/rate-limit-throttling.md)
- [Pinwheel Credential Spray](cookbook/pinwheel-credential-spray.md)
- [Output Body to File](cookbook/output-to-file.md)
- [Email Link Extraction](cookbook/email-link-extraction.md)
- [Special Wordlists](cookbook/special-wordlists.md)

## Code References
- Context menu entry in Burp: `src/OfferTurbo.kt:12–17`
- Attack flow and UI: `src/fast-http.kt:364–441`
- Status/RPS string: `src/RequestEngine.kt:354–365`
- Script environment helpers: `resources/ScriptEnvironment.py:3–335`
- BURP engines batching/gating: `src/BurpRequestEngine.kt:111–176`
- THREADED pause/partial read: `src/ThreadedRequestEngine.kt:253–292, 430–459, 546–567`
- HTTP/2 connection management: `src/HTTP2RequestEngine.kt:39–82`; streams `src/Stream.kt:27–106`
- Floodgate/gating mechanics: `src/burp/Floodgate.java:23–81`