# AGENT.md

This file provides guidance to coding agents when working with code in this repository.

## Repository Overview

Personal resume website for Pushpender Sharma, hosted at https://ipushpie.github.io via GitHub Pages. The repo has two independent deliverables:

1. **`index.html`** — Single-file portfolio website (HTML + CSS + JS, no build step)
2. **`resume.tex`** — LaTeX resume compiled to `Pushpender_resume.pdf`

## Editing the Resume (LaTeX)

Source files:
- `resume.tex` — Content (sections, experience, skills, etc.)
- `resume.cls` — Custom LaTeX class defining layout/styles (rarely edited)

To compile locally (requires a LaTeX distribution with `pdflatex`):
```sh
pdflatex resume.tex
mv resume.pdf Pushpender_resume.pdf
```

**CI auto-compilation:** Pushing changes to `resume.tex` or `resume.cls` triggers `.github/workflows/compile-resume.yml`, which compiles via `xu-cheng/latex-action@v3` (pdflatex engine) and auto-commits the updated `Pushpender_resume.pdf`. Do not manually commit the PDF — let CI handle it.

## Editing the Portfolio Website

`index.html` is entirely self-contained — all CSS and JavaScript are inline. No build tools, bundlers, or package managers are used. Open directly in a browser to preview:
```sh
open index.html
```

Key design system (CSS variables in `:root`):
- Colors: `--navy` (#0a192f), `--green` (#64ffda) as accent
- Fonts: Inter (body), JetBrains Mono (code/mono elements)
- External deps loaded from CDN: Google Fonts, devicons (devicon.min.css)

The page includes animated floating tech icons (DOM/CSS transform-based), a cursor spotlight effect, and scroll-triggered section reveals — all implemented in vanilla JS at the bottom of `index.html`.

## Architecture Notes

- There is no local build system, test suite, or linting config.
- GitHub Pages serves `index.html` from the `main` branch root directly.
- The PDF is committed as a binary asset (`Pushpender_resume.pdf`) served alongside the HTML.
