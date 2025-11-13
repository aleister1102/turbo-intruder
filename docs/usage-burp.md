# Using in Burp

- Choose insertion point by selecting text in the request before opening Turbo Intruder (src/fast-http.kt:326–333).
- Adjust target service (host, port, protocol) in the top controls (src/fast-http.kt:283–297).
- Load scripts: pick built-in examples or your script directory (src/fast-http.kt:181–190, 485–517).
- Start/stop:
  - `Attack` starts; `Halt` cancels; `Configure` resets UI (src/fast-http.kt:375–397).
  - Status string includes queue size, duration, RPS (src/AttackHandler.kt:33–43; src/RequestEngine.kt:354–365).
- Bulk mode: run against multiple selected requests via context menu (src/OfferTurbo.kt:22–31).
- Table actions: select and export, sort, view details; anomaly rank auto-sorts in newer Burp versions (src/RequestEngine.kt:336–347).