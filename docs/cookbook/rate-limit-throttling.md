# Rate-Limit Throttling

- Per-request sleeps and periodic pauses between batches (resources/examples/ratelimit.py).

```python
for word in open('words.txt'):
    time.sleep(throttleMillisecs/1000)
    engine.queue(target.req, word.rstrip())
    n += 1
    if n == triedWords:
        time.sleep(secs)
        n = 0
```