# Partial Read Token Capture

- Capture tokens from partial socket reads using `readCallback` (resources/examples/partialReadCallback.py).

```
engine = RequestEngine(endpoint=target.endpoint,
                       concurrentConnections=2,
                       readCallback=handleRead,
                       readSize=256)
engine.queue(target.req)

def handleRead(data):
    if 'token' in data:
        engine.queue('something-using-the-token')
```