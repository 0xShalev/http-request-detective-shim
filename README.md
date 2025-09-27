# HTTP Request-Detective JS Shim

Lightweight shim that instruments `fetch` and `XMLHttpRequest` in the browser to capture the *initiator* stack for each outbound request and log a compact, readable report to the console:

```
[2025-09-27T12:34:56.789Z] POST https://api.example.com/endpoint
    - https://site.com/app.js:123:45
    - https://lib.cdn.com/lib.min.js:10:200
```

> The script uses **stacktrace.js** (ErrorStackParser) under the hood to parse and normalize stack traces across browsers, so you get consistent `file:line:column` frames even when formats differ.

---

## Features
- Instruments both modern `fetch` and legacy `XMLHttpRequest`.
- Non-intrusive: wrapped code is try/catch guarded so it won’t break the host app.
- Small and easy to drop into a page (can be injected as a `<script>`).

---

## Installation

### Paste to console

You can just paste the js itself into the console and automaticly will wrap all relavant instruments

### Load as inline
Include the script - preferably should be the first `<script>`

```html
<script src="path/to/initiator-capture.js"></script>
```

---
