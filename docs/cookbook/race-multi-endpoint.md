# Race: Multi-Endpoint

- Queue mixed methods and paths, then open the gate (resources/examples/race-multi-endpoint.py).

```python
req1 = r'''GET /static/robots.txt?%s=test HTTP/1.1
Host: hackxor.net

'''
req2 = r'''POST /static/robots.txt?%s=test HTTP/1.1
Host: hackxor.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 0

'''
for i in range(5):
    engine.queue(req1, 'search', gate='race1')
    engine.queue(req2, 'hidden', gate='race1')
engine.openGate('race1')
```