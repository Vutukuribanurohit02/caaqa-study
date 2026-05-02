# CAAQA Interview Study Companion

> An interactive interview-prep companion to \*\*Hennessy \&amp; Patterson's \_Computer Architecture: A Quantitative Approach\_ (5th Ed., 2012)\*\* — the field's standard graduate-level text. This is the second site in a study-guide series after my \[Modern Processor Design (Shen \&amp; Lipasti)](https://github.com/Vutukuribanurohit02/processor-design-study) site.

**Live site:** *https://vutukuribanurohit02.github.io/caaqa-study/*
---

## What's inside

* **9 chapters covered** — Chapters 1–6 plus Appendices A, B, C
* **31 interview-grade Q\&A** — written the way you would actually answer in a panel
* **42 spaced-repetition flashcards** — quick-recall format for term/concept drilling
* **20 multiple-choice quiz items** — with explanations, randomized order, and persistent score history
* **Universal search** — across chapters, Q\&A, concepts, and flashcards in real time
* **Progress dashboard** — flashcard mastery, quiz history, per-chapter stats
* **Light/dark theme** with persistent preference

## What's new vs v1 (Modern Processor Design site)

The v1 site was a single static HTML file with all content inlined — fast to ship, but every content edit meant scrolling through 2,000+ lines of markup. This v2 fixes that with a clean **frontend ↔ data separation**:

```
caaqa-site/
├── index.html        ← UI / renderer / app logic
└── data/
    ├── chapters.json ← chapter metadata + key concepts
    ├── qa.json       ← interview Q\&A by chapter
    ├── flashcards.json
    └── quiz.json     ← MCQ with explanations
```

This means:

* **Adding a Q\&A** is one edit to `data/qa.json` — no UI risk
* **The renderer fetches data files in parallel** at page load (`Promise.allSettled`), so total round-trip is \~1 file's latency, not 4×
* **Failure is graceful** — if a data file 404s, the rest of the site still works and an error message appears
* **The architecture is API-ready** — replacing `fetch('data/qa.json')` with `fetch('/api/qa')` is a one-line change if a real backend is added later (e.g., AI-generated questions from Claude API)

Other upgrades:

* **Spaced-repetition flashcards** — cards marked "review" come back sooner; "got it" cards retire
* **Quiz score history** — last 50 attempts saved; average and best surfaced on the dashboard
* **Search-as-you-type** with live highlighting
* **Editorial typography** — Fraunces (display serif) + Inter Tight (body) + JetBrains Mono (technical labels)
* **Mobile-first responsive layout** with proper hamburger menu and touch targets

## Quick start

### Option A — view locally

```bash
git clone https://github.com/Vutukuribanurohit02/caaqa-study.git
cd caaqa-study
python3 -m http.server 8000
# open http://localhost:8000
```

> \*\*Note:\*\* opening `index.html` directly with `file://` will fail because browsers block JSON `fetch()` from local files due to CORS. Use a local server or push to GitHub Pages.

### Option B — deploy to GitHub Pages

1. Push the repo to GitHub
2. Settings → Pages → Source: `Deploy from a branch` → `main` / `(root)`
3. Wait \~30 seconds — your site is live at `https://<username>.github.io/caaqa-study/`

## Design philosophy

This guide is for hardware engineers preparing for **ASIC, RTL, verification, SoC, and physical design** interviews where computer architecture comes up in questions like:

* "Walk me through Tomasulo's algorithm."
* "Explain the difference between snooping and directory cache coherence."
* "What's the difference between sequential consistency and TSO?"
* "When would you choose write-back over write-through?"

Each Q\&A is sized to the response a panel actually wants — typically 30–90 seconds spoken, technical but not lecture-length. Where there's a famous diagram or example (the 5-stage MIPS pipeline, MESI state transitions, the Roofline model), the answer references it explicitly so you have shared vocabulary with the interviewer.

## How to use this guide

**Three-pass method** works well:

1. **Skim** — read each chapter's summary and key-concepts list. Build a map of what's covered. (\~30 min total)
2. **Deep read** — open every Q\&A under the chapters most relevant to your target role. Try answering aloud before reading. (\~1–2 hours per chapter)
3. **Active recall** — use Flashcards mode for 10 min before each interview. Take a Quiz to find weak spots, then revisit those chapters.

**One-week prep order** (encoded in the site's home page):

|Day|Focus|Why|
|-|-|-|
|1–2|Appendix C (pipelining) → Chapter 3 (ILP)|Foundation for every digital design question|
|3|Appendix B → Chapter 2 (memory)|Caches are the most-asked topic, period|
|4|Chapter 5 (multicore, coherence)|Increasingly common in modern interviews|
|5|Chapter 1 (performance, power, Amdahl)|Framework for explaining tradeoffs|
|6–7|Chapters 4 (DLP/GPU) + 6 (WSC)|Breadth; quiz weak areas|

## Tech stack

* **Single static HTML** + **4 JSON data files** + zero dependencies
* All progress (flashcard mastery, quiz history, theme) stored in browser `localStorage`
* \~80 KB compressed; loads in under 1 second on most connections
* Works offline once loaded (except first fetch of JSON files)
* No tracking, no analytics, no ads, no cookies

## About

Built by **Banu Rohit Vutukuri** — MS Electrical Engineering (Computer \& Embedded Systems), University of Houston, December 2025. Targeting RTL Design Verification, SoC Integration, and Physical Design roles.

[LinkedIn](https://www.linkedin.com/in/banurohit-vutukuri/) · [GitHub](https://github.com/Vutukuribanurohit02) · vutukuribanurohit02@gmail.com

## Citation \& copyright

All concepts, frameworks, and pedagogy are credited to the original authors:

> Hennessy, J. L., \&amp; Patterson, D. A. \_Computer Architecture: A Quantitative Approach.\_ Fifth Edition. Morgan Kaufmann / Elsevier, 2012. ISBN 978-0-12-383872-8.

This guide is an **independent study companion**, not a replacement. Q\&A answers, summaries, and explanations are written from scratch in my own words for interview-prep context. **Buy the textbook** if you want full depth — it remains the definitive reference for graduate computer architecture.

The site contains **no verbatim text from the book**, no figures or diagrams reproduced from the book, and no extended quotations. It is offered free for educational use.

\---

*If this guide helps you land a role, drop me a note — I'd love to hear.*

