# Request Reference

- Attributes:
  - `status`/`code`, `length`, `wordcount` (src/Request.kt:35–39).
  - Timing: `time` (µs), `sent`, `arrival`, `connectionID`, `order` (src/BurpRequestEngine.kt:154–173; src/ThreadedRequestEngine.kt:480–488).
- Response:
  - `response` is headers + body; decompression handled for gzip/deflate/br (src/ThreadedRequestEngine.kt:69–95, 474–475).
- Metadata:
  - `label` for grouping; `learnBoring` baseline; `montoyaReq` reference (src/Request.kt:9–33, 83–88).
- Content-Length handling:
  - Auto-fixed unless `fixContentLength=False` (src/Request.kt:124–147).
  - Manual header update via `setHeader()` (src/Request.kt:148–163).
- Burp conversion:
  - `getBurpRequest()` and Montoya mapping for anomaly ranking (src/Request.kt:79–88; src/RequestEngine.kt:336–347).