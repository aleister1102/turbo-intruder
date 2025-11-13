# Multiple Parameters

- Inject two payloads into two `%s` markers (resources/examples/multipleParameters.py).

```
for firstWord in open('/usr/share/dict/words'):
  for secondWord in open('/usr/share/dict/american-english'):
    engine.queue(target.req, [firstWord.rstrip(), secondWord.rstrip()])
```