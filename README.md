# Interactive Learning Doc

Turn a book PDF into an interactive, **source-grounded** study workspace — entirely in your browser. The **full original text is preserved**; alongside it the AI adds a study layer: **key points**, **key concepts** with inline links + backlinks, **comprehension quizzes**, **math/LaTeX rendering** (KaTeX), and an **Obsidian-style concept network** (a **draggable** force-directed graph). Three-pane, **fully responsive** layout (phone / tablet / desktop): a sidebar (contents + concepts + actions), the original book in the centre, and the AI study rail on the right. **Figures and tables are preserved** — each section links to the original **page image**, so anything text extraction can't capture is never lost. You choose your **provider (OpenAI / Gemini), model, and key** — the key stays in your browser. The built-in sample is a standard accounting chapter (NCERT "Accounting for Partnership: Basic Concepts").

No backend. No server. Nothing is uploaded anywhere except the calls your browser makes directly to the AI provider you choose, using your own key.

## Try it without a key

Open the page and click **“Open a sample interactive doc (no API key)”**, or append `#demo` to the URL. A bundled public-domain sample renders instantly — no key, no network needed.

## Use it on your own book

1. Pick your **provider** (ChatGPT / OpenAI or Gemini), paste your **API key**, and choose a **model** (click *Load my models* to list them from your account).
2. **Drop a PDF** (or click to choose).

Then read the full text with highlights and concept links, use the per-section study rail (key points, concepts, quizzes), click a concept for its backlinks, or open **Graph** for the draggable network.

**Bring a book you have the rights to** (official / public-domain / your own). Don’t upload documents containing personal identifiers (e.g. Aadhaar, PAN, full bank-account numbers) — the text is sent to your chosen AI provider.

## How it protects the source

- **No content lost** — the complete original text of every section is shown, unchanged; the AI only adds a study layer beside it.
- **Images & tables preserved** — every section links to the original **page image** (rendered from the PDF), so figures and tables that text extraction can't reproduce are kept intact.
- **Grounded highlights & study layer** — every key point, concept, and quiz quotes an exact substring of the source (used both to highlight the sentence and to verify grounding); anything not found in the source is dropped.
- **Strict verify (on)** — a second AI pass drops any claim not supported by its source span.
- **Provenance** — concepts are badged “from the book” vs “general knowledge”.

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
