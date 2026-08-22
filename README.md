# Interactive Learning Doc

Turn a book PDF into an interactive, **source-preserving** learning document — entirely in your browser. Upload a PDF, use your own Gemini or OpenAI API key, and get a reader with inline definitions, comprehension checks, and plain-language notes layered on top of the **original text (kept verbatim, in full)**.

No backend. No server. Nothing is uploaded anywhere except the calls your browser makes directly to the AI provider you choose, using your own key.

## Try it without a key

Open the page and click **“Open a sample interactive doc (no API key)”**, or append `#demo` to the URL. A bundled public-domain sample renders instantly — no key, no network needed.

## Use it on your own book

1. Choose a provider (ChatGPT / OpenAI or Gemini).
2. Paste your API key (it stays in your browser).
3. Pick a model (the list is fetched from your account).
4. Upload a PDF and generate.

**Bring a book you have the rights to** (official / public-domain / your own). Don’t upload documents containing personal identifiers (e.g. Aadhaar, PAN, full bank-account numbers) — the text is sent to your chosen AI provider.

## How it protects the source

- **Originality preserved** — the model never rewrites the book; it only adds a labelled overlay. The original text is displayed verbatim and in full.
- **No detail lost** — every section is shown; sections beyond the cost cap appear as plain text.
- **Grounding gate** — every AI item must quote an exact substring of the source, or it is dropped.
- **Strict verify (optional)** — a second AI pass drops any claim not supported by its source span.
- **Provenance** — definitions are badged “from the book” vs “general knowledge”; quizzes cite their source span.

## Deploy to GitHub Pages

Only `index.html` is required at runtime (the demo is embedded). `.nojekyll` is included so Pages serves files as-is.

```bash
git init
git add index.html .nojekyll README.md
git commit -m "Interactive learning doc"
git branch -M main
git remote add origin https://github.com/<you>/<repo>.git
git push -u origin main
```

Then in the repo: **Settings → Pages → Build and deployment → Source: “Deploy from a branch” → Branch: `main` / `/ (root)` → Save.**
Your site will be at `https://<you>.github.io/<repo>/` (and the demo at `…/#demo`).

> Hosting over HTTPS (as Pages does) also makes the provider API calls work more reliably than opening the file locally.

## Privacy

The page is static. Your API key is held only in your browser’s memory (and, if you tick “remember”, in that browser’s `localStorage` on your own device). It is sent only to the provider’s API endpoint — never to this site’s host or anyone else.

## Local development

```bash
python3 -m http.server 8000
# open http://localhost:8000  (or http://localhost:8000/#demo)
```

## Files

- `index.html` — the entire app (self-contained; only runtime file needed).
- `.nojekyll` — GitHub Pages: serve files as-is.
- `build.py`, `generate_preview.py`, `inject_demo.py`, `book.*`, `*.png` — local test/scaffolding artifacts, not needed for hosting.
