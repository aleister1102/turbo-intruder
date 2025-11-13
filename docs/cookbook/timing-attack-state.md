# Timing Attack with State

- Use labels and `engine.userState` to compare timings (resources/examples/timingAttackWithState.py).

```python
engine.userState['base_times'] = []
for i in range(20):
    engine.queue(target.req, randstr(i), label='benchmark')
...
if req.label == 'benchmark':
    req.engine.userState['base_times'].append(req.time)
elif req.time > max(req.engine.userState['base_times'])+10:
    table.add(req)
```