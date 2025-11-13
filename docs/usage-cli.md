# CLI Usage

- Command:

```
java -jar turbo.jar <scriptFile> <baseRequestFile> <endpoint> <baseInput>
```

- Example:

```
java -jar turbo.jar resources/examples/basic.py resources/examples/request.txt https://example.net:443 foobar
```

- Behavior and notes:
  - SSL/TLS handling differs slightly outside Burp (src/fast-http.kt:540–541).
  - Input requests are normalized to CRLF (`\r\n`) if needed (src/fast-http.kt:541–544).
  - Output is printed to console via `ConsolePrinter`.