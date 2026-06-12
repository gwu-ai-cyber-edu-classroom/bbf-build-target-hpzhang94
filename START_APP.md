# START_APP.md — how to run and probe this app

> **Build team:** fill in every `<...>` below once your app runs. Other teams use this file to
> start your app and probe it during Break. Keep it accurate — a break is filed against the app a
> breaker can actually start from these instructions.

## What this app is

- **App:** a URL shortener service (menu #3) — shorten a long URL to a short code, follow the code to redirect.
- **Stack:** Python + Flask (storage: SQLite file `links.db`, auto-created on first run).

## Start it

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Run it
flask --app app run --port 8000
# (or: python app.py)
```

- **Base URL:** http://localhost:8000
- **Stop it:** Ctrl-C in the terminal running it.

## How to interact with it

- **Main endpoints / pages:**
  - `GET /` — home page: a form to shorten a URL and a list of recent public links.
  - `POST /shorten` — create a short link from a long URL. Form fields `url` (required) and `title` (optional); also accepts JSON `{"url": "..."}`. Returns JSON `{code, short_url, long_url}`.
  - `GET /<code>` — follow a short code; 302-redirects to the stored long URL (404 if unknown).
  - `GET /api/links/<code>` — JSON info/stats for a single short code (`long_url`, `title`, `clicks`, …).
- **Accounts / credentials for legitimate use** (if the app has login): none.
- **A benign request that should succeed:**

  ```bash
  curl -i http://localhost:8000/py          # redirects to https://www.python.org/
  curl -s -X POST http://localhost:8000/shorten -d 'url=https://example.com&title=Example'
  ```

## For breakers

Attack this **running app over HTTP** — do **not** read this repo's source or `secret/` to find a
break. See [AGENTS_BREAK.md](AGENTS_BREAK.md) for the rules and your AI agent's instructions, and
[SPEC.md](SPEC.md) for the five properties (P1–P5) you are probing for.
