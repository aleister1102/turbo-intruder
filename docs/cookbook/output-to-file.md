# Output Body to File

- Write interesting response bodies to a file (resources/examples/outputToFile.py).

```python
if interesting:
    header, _, body = req.response.partition('\r\n\r\n')
    with open('/tmp/output-turbo.txt', 'a+') as f:
        f.write(body + "\n")
```