# AI Assisted Coding workbook

Exercise instructions for the course "Einstieg in AI Assisted Coding mit GitHub Copilot",
published at https://cgamperl.github.io/ai-coding-workbook/.

## Layout

- `workbook/docs/*.md`: the pages (German). `index.md` start page, `uebungen.md` exercises 1–8,
  `zusatz.md` extra exercises.
- `workbook/docs/.vitepress/config.mts`: VitePress configuration; the sidebar lists every
  `### …` heading of `uebungen.md` and `zusatz.md`, generated at build time.
- `workbook/docs/public/downloads/calculator.zip`: unchanged start.spring.io project
  (Gradle Kotlin DSL, Java 21, Spring Boot 4.1.2, no dependencies), fallback for exercise 1.

## Publishing

A push to `main` that changes `workbook/` builds the site and deploys it to GitHub Pages
(workflow `.github/workflows/workbook.yaml`, Pages source "GitHub Actions"). The site is
live one to two minutes after the push. Browsers may cache pages for up to 10 minutes;
an open page may need a reload with Ctrl+F5.

## Local preview

Node 22 or newer:

```bash
cd workbook
npm ci
npm run dev                         # live preview while editing
npm run build && npm run preview    # the published build
```

`http://localhost:…` links are not checked; any other dead link fails the build.
