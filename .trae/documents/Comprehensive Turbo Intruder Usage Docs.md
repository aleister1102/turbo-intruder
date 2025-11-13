# Docs Folder Structure
- quickstart.md – getting started in Burp and CLI
- usage-burp.md – how to run attacks from Burp UI, selection, scripts
- usage-cli.md – CLI invocation, arguments, examples
- concepts.md – core ideas: engines, requests, payloads, gates, labels, baselines
- python-api.md – ScriptEnvironment helpers, decorators, Engine enum, RequestEngine constructor & queue params
- engines.md – BURP / BURP2 / THREADED / HTTP2 comparison, capabilities & limitations
- request-reference.md – `Request` attributes, lifecycle, response handling, anomaly ranking
- advanced-techniques.md – gates, pause markers, partial reads, endpoint overrides, autoStart vs start
- http2-notes.md – HTTP/2 specifics, header rewrites, pseudo-headers, single-packet attack
- performance-tuning.md – concurrency, pipeline, readSize, timeouts, retries
- cookbook/ – recipe pages covering common attacks (one file per recipe)
- troubleshooting.md – common errors, deadlocks, timeouts, retries, missing CL

# Content Outline
## quickstart.md
1. Install and open from Burp: right-click → "Send to turbo intruder" (src/OfferTurbo.kt:12–17)
2. Script shape: `queueRequests(target, wordlists)` and `handleResponse(req, interesting)` with example (resources/examples/default.py)
3. Minimal brute-force with `Engine.THREADED` and `table.add(req)`
4. Verify results: table view, status string, RPS (src/RequestEngine.kt:354–365)

## usage-burp.md
- Selecting insertion point from highlighted request (src/fast-http.kt:326–333)
- Changing host/port/protocol before running (src/fast-http.kt:283–297, 399–430)
- Loading built-in examples and custom script directory (src/fast-http.kt:181–190, 485–517)
- Starting/stopping/halting attacks; status messages (src/AttackHandler.kt:33–56)
- Bulk mode for multiple selected requests (src/OfferTurbo.kt:22–31)

## usage-cli.md
- Command: `java -jar turbo.jar <scriptFile> <baseRequestFile> <endpoint> <baseInput>` (src/fast-http.kt:554–556)
- Notes on SSL differences outside Burp and CRLF normalization (src/fast-http.kt:540–544)
- Example using `resources/examples/request.txt` and `resources/examples/basic.py`

## concepts.md
- Engines and what they target (resources/ScriptEnvironment.py:258–264)
- Request queuing with `%s` markers and payload substitution (src/Request.kt:99–110)
- Labels and `engine.userState` for stateful attacks (resources/examples/timingAttackWithState.py:8–23)
- Baseline learning via `learn=N` and response variation analysis (src/RequestEngine.kt:371–401)
- Output and `table.add(req)` behavior

## python-api.md
- Decorators: `MatchStatus`, `MatchRegex`, `FilterSizeRange`, `UniqueWordCount`, etc. (resources/ScriptEnvironment.py:3–141, 144–231)
- Helpers: `randstr`, `mean`, `stddev` (resources/ScriptEnvironment.py:233–247)
- Engine enum: BURP, THREADED, HTTP2, BURP2, SPIKE (resources/ScriptEnvironment.py:258–264; SPIKE is experimental)
- RequestEngine constructor args and semantics, including `readCallback`, `readSize`, `autoStart` (resources/ScriptEnvironment.py:267–307)
- `queue()` parameters: payloads, `learn`, per-request `callback`, `gate`, `label`, `pauseBefore`, `pauseTime`, `pauseMarker`, `delay`, `endpoint`, `fixContentLength` (resources/ScriptEnvironment.py:309–315; src/RequestEngine.kt:93–131)
- `openGate`, `applySetting`, `start`, `complete`, `cancel` (resources/ScriptEnvironment.py:317–334)
- Wordlists object fields: `bruteforce`, `observedWords`, `clipboard` (src/fast-http.kt:58–73); bruteforce example (resources/ScriptEnvironment.py:249–257)

## engines.md
- BURP (HTTP/1) and BURP2 (HTTP/2) using Burp’s stack; batch gating behavior (src/BurpRequestEngine.kt:14–17, 111–176)
- THREADED custom TCP engine, pipeline and socket-level controls (src/ThreadedRequestEngine.kt:18–24, 130–137)
- HTTP2 custom engine; connection management and retries (src/HTTP2RequestEngine.kt:16–37, 59–82)
- Limitations: BURP engine forces no pipelining/1 req per connection (resources/ScriptEnvironment.py:281–286)
- SPIKE mention as experimental/unavailable in current build (src/SpikeEngine.kt shows commented implementation)

## request-reference.md
- Core attributes: `status`, `length`, `wordcount` (src/Request.kt:35–39)
- Timing fields: `time` (µs), `sent`, `arrival`, `connectionID`, ordering (src/BurpRequestEngine.kt:154–173; src/ThreadedRequestEngine.kt:480–488)
- `response` content and compression handling (src/ThreadedRequestEngine.kt:69–95, 474–481)
- `label`, `engine.userState` and per-request `callback`
- Content-Length auto-fixing behavior and override via `fixContentLength` (src/Request.kt:124–147)

## advanced-techniques.md
- Gates: sync attacks and race conditions with `gate` and `openGate()` (resources/examples/race-single-packet-attack.py:11–19; src/burp/Floodgate.java:23–81)
- Pause and probe: `pauseBefore`, `pauseMarkers`, and `pauseTime` (src/RequestEngine.kt:123–128; src/ThreadedRequestEngine.kt:253–292, 546–567)
- Partial read callbacks: `readCallback(data)` and `readSize` (resources/examples/partialReadCallback.py)
- Endpoint overrides per request (src/BurpRequestEngine.kt:199–222)
- Auto-start vs manual `start(timeout)` and `idleTimeout` cancellation (resources/ScriptEnvironment.py:303–327; src/RequestEngine.kt:196–204)

## http2-notes.md
- Header rewrites for HTTP/2 engines: `^`→`\r`, `~`→`\n`, `` ` ``→`:`; pseudo-headers override (resources/examples/http2.py:8–14)
- Single-packet technique via BURP2 gates (resources/examples/race-single-packet-attack.py:3–9)
- Connection pool and stream lifecycle (src/HTTP2RequestEngine.kt:16–37; src/Stream.kt:27–106)

## performance-tuning.md
- `concurrentConnections`, `requestsPerConnection`, `pipeline` (resources/examples/default.py; src/ThreadedRequestEngine.kt)
- `readSize`, socket timeouts, `resumeSSL` reuse, `explodeOnEarlyRead` (src/ThreadedRequestEngine.kt:18, 431–459)
- Queue sizing and backpressure (src/RequestEngine.kt:154–177)
- Retries and permanent failures (src/RequestEngine.kt:404–426, 29–31)

## cookbook/
- basic-bruteforce.md (resources/examples/basic.py)
- multiple-parameters.md (resources/examples/multipleParameters.py)
- http2-wordlist.md (resources/examples/http2.py)
- race-single-packet.md (resources/examples/race-single-packet-attack.py)
- race-multi-endpoint.md (resources/examples/race-multi-endpoint.py)
- timing-attack-state.md (resources/examples/timingAttackWithState.py)
- partial-read-token.md (resources/examples/partialReadCallback.py)
- rate-limit-throttling.md (resources/examples/ratelimit.py)
- pinwheel-credential-spray.md (resources/examples/pinwheel.py)
- output-to-file.md (resources/examples/outputToFile.py)
- email-link-extraction.md (resources/examples/email-link-extraction.py)
- special-wordlists.md (resources/examples/specialWordlists.py)

## troubleshooting.md
- Deadlocks from gated requests vs `concurrentConnections` (src/RequestEngine.kt:142–145)
- "No %s injection markers" and payload mismatches (src/RequestEngine.kt:99–106)
- Missing Content-Length and slow reads; switch engines or set `ignoreLength` (src/ThreadedRequestEngine.kt:430–459; `applySetting("ignoreLength", true)` available via `applySetting`) (src/RequestEngine.kt:428–434)
- Connection drops and retries behavior (src/HTTP2RequestEngine.kt:63–76; src/ThreadedRequestEngine.kt:495–539)
- Burp version requirements for HTTP/1 `makeHttpRequest` and anomaly ranking (src/BurpRequestEngine.kt:73–76; src/RequestEngine.kt:322–334)

# Writing Approach
- Create `docs/` with the files above; keep example-driven and concise.
- Use consistent code blocks with inline literals; avoid heavy formatting.
- Cross-link recipes to the APIs they use; reference exact code locations using `file_path:line_number` format.
- Include warnings where an engine disables features (e.g., BURP enforcing 1 req/connection).

# Verification
- Open each recipe in Burp using built-in examples to confirm steps mirror behavior.
- Validate CLI examples against `main()` and sample request.
- Sanity-check API references against current source files and example scripts.
- Ensure no secrets or environment-specific paths are committed; keep paths generic.

# Next Steps
- Implement the docs files and wire internal links.
- Review phrasing for clarity and completeness.
- Iterate with user feedback to fill any remaining gaps.