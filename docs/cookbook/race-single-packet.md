# Race: Single-Packet Attack

- For HTTP/2 targets, use `Engine.BURP2` with gates (resources/examples/race-single-packet-attack.py).

```
engine = RequestEngine(endpoint=target.endpoint,
                       concurrentConnections=1,
                       engine=Engine.BURP2)
for i in range(20):
    engine.queue(target.req, gate='race1')
engine.openGate('race1')
```