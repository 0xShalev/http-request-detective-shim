# HTTP Request Detective JS Shim

Lightweight, drop-in shim that instruments `fetch` and `XMLHttpRequest` in the browser to capture the initiator stack for each outbound request and print a compact, readable report to the console.

```
[2025-09-27T12:34:56.789Z] POST https://api.example.com/endpoint
    - https://site.com/app.js:123:45
    - https://lib.cdn.com/lib.min.js:10:200
```

> The script embeds **ErrorStackParser** from [stacktrace.js](https://github.com/stacktracejs/stacktrace.js) to parse and normalize stack traces across browsers, producing consistent `file:line:column` frames even when formats differ.

---

## Features
- Instruments both modern `fetch` and legacy `XMLHttpRequest`.
- Non-intrusive: wrappers are try/catch-guarded so they won’t break the host app.
- Tiny, single file that you can paste into the console or inject as a `<script>`.

---

## Usage

### Quick: paste into the console
Copy the contents of `shim.js` and paste it into the page’s DevTools console. It will automatically wrap `fetch` and `XMLHttpRequest` on that page.

### As a script tag
Include the script as early as possible (ideally before other scripts) so more requests are captured:

```html
<script src="/path/to/shim.js"></script>
```

---

## Notes
- Captures up to 5 stack frames by default. You can adjust `MAX_STACKTRACE_FRAMES` in `shim.js` if needed.
- Attempts to log the request URL and HTTP method when available for both `fetch` and XHR. Some call patterns (e.g., `fetch` invoked with a URL string) may not expose the method; the request still proceeds unaffected.

## Browser support
Chrome 1+, Firefox 3.6+, Safari 7+, Opera 9+, IE 10+, iOS 7+, Android 4.2+ (via ErrorStackParser)

## License
See `LICENSE`.
