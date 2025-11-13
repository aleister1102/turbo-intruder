# HTTP/2 Wordlist

- Use `Engine.HTTP2`; note header rewrites and pseudo-headers (resources/examples/http2.py:1–17).

```python
engine = RequestEngine(endpoint=target.endpoint,
                       concurrentConnections=5,
                       requestsPerConnection=100,
                       engine=Engine.HTTP2)
for word in open('/usr/share/dict/words'):
    engine.queue(target.req, word.rstrip())
```