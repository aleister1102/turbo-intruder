# Quickstart

- Open in Burp: right-click a request → `Send to turbo intruder` (src/OfferTurbo.kt:12–17).
- Script shape: define `queueRequests(target, wordlists)` and `handleResponse(req, interesting)`.
- Minimal example:

```
def queueRequests(target, wordlists):
    engine = RequestEngine(endpoint=target.endpoint,
                           concurrentConnections=5,
                           requestsPerConnection=100,
                           pipeline=False,
                           engine=Engine.THREADED)
    for word in open('/usr/share/dict/words'):
        engine.queue(target.req, word.rstrip())

def handleResponse(req, interesting):
    table.add(req)
```

- Run: click `Attack` in the Turbo Intruder window (src/fast-http.kt:364–441).
- See results: requests appear in the table; status shows RPS and progress (src/RequestEngine.kt:354–365).
- Alternative: use CLI if not in Burp; see [CLI Usage](usage-cli.md).