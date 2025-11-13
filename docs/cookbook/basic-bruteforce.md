# Basic Bruteforce

- Use `Engine.THREADED` with a wordlist (resources/examples/basic.py).
- Key lines:

```python
engine = RequestEngine(endpoint=target.endpoint,
                       concurrentConnections=5,
                       requestsPerConnection=100,
                       pipeline=False,
                       engine=Engine.THREADED)
for word in open('/usr/share/dict/words'):
    engine.queue(target.req, word.rstrip())
```