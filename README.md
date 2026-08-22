# Interactive Learning Doc

Turn a book PDF into an interactive, **source-grounded** learning document — entirely in your browser. The only input is a **PDF**: it surfaces the **important points** as an interactive summary — with the **original wording preserved verbatim for the things that matter** (definitions, rules, key figures), key terms, comprehension checks, **math/LaTeX rendering** (via KaTeX), and an **Obsidian-style concept network** (inline concept links with backlinks, plus a **draggable** force-directed graph view). One-time: paste your own Gemini or OpenAI key (auto-detected, saved in your browser); after that it's just drop-a-PDF.

No backend. No server. Nothing is uploaded anywhere except the calls your browser makes directly to the AI provider you choose, using your own key.

## Try it without a key

Open the page and click **“Open a sample interactive doc (no API key)”**, or append `#demo` to the URL. A bundled public-domain sample renders instantly — no key, no network needed.

## Use it on your own book

1. **First time only:** paste your OpenAI (`sk-…`) or Gemini (`AIza…`) key — the provider is auto-detected and the key is saved in your browser.
2. **Drop a PDF** (or click to choose). That's the only input — provider, model, chunking, summary depth, and verification are all automatic.

Then read the summary, click concept links to see where each idea recurs, or open **Graph** for the network view.

**Bring a book you have the rights to** (official / public-domain / your own). Don’t upload documents containing personal identifiers (e.g. Aadhaar, PAN, full bank-account numbers) — the text is sent to your chosen AI provider.

## How it protects the source

- **Summarised, not rewritten wholesale** — the reader shows the important points, not the full body text.
- **Original wording preserved for what matters** — important points (definitions, rules, exact figures) are shown **verbatim in quotes**, cited to the page; other points have a “show original” toggle.
- **Grounding gate** — every point, definition, and quiz must quote an exact substring of the source, or it is dropped.
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
