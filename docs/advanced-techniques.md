# Advanced Techniques

- Gates for synchronized sends:
  - Queue with `gate='race1'` then `engine.openGate('race1')` (resources/examples/race-single-packet-attack.py:11–19).
  - Gate mechanics and deadlock prevention (src/burp/Floodgate.java:23–81; src/RequestEngine.kt:142–145).
- Pausing:
  - `pauseBefore` byte offset or negative-from-end; `pauseMarkers` to pause after markers; `pauseTime` in ms (src/RequestEngine.kt:123–128; src/ThreadedRequestEngine.kt:253–292, 546–567).
- Partial reads:
  - `readCallback(data)` for token capture; `readSize` buffer tuning (resources/examples/partialReadCallback.py).
- Endpoint overrides:
  - Per-request `endpoint` targets another host/service (src/BurpRequestEngine.kt:199–222).
- Start modes and timeouts:
  - `autoStart=True/False`, manual `start(timeout)`; total `idleTimeout` cancels inactive attacks (resources/ScriptEnvironment.py:303–327; src/RequestEngine.kt:196–204).