# CanLawTex

A LaTeX template for Canadian legal writing that implements footnote-based citations
following the **Canadian Guide to Uniform Legal Citation (McGill Guide, 9th ed.)**.

This repository is organized around a single manuscript build. The thesis depends
on only four source files, and unused standalone formatting experiments have been
removed so the workspace stays focused.

## Core Files

| File | Purpose |
|------|---------|
| `legalcite.sty` | Citation package for McGill-style footnotes and authorities |
| `main.tex` | Document shell: packages, title, abstract, bibliography |
| `sources.tex` | Source declarations used by the manuscript |
| `body.tex` | Thesis body content |
| `main.pdf` | Current compiled manuscript output (optional to track) |

## Project Rules

- Keep `main.tex`, `body.tex`, `sources.tex`, and `legalcite.sty` in the repo root unless you also plan to update the manuscript entrypoint.
- Treat `.aux`, `.log`, `.out`, `.toc`, and similar files as disposable build artifacts.
- Remove experimental scratch files once they are no longer part of the manuscript workflow.

## Quick Start

1. Open `sources.tex` and declare your sources.
2. Open `body.tex` and write the paper using `\legal{}`, `\legalname{}`, and `\legalshort{}`.
3. Compile with `pdflatex` twice:

```text
pdflatex main.tex
pdflatex main.tex
```

## Declaring Sources

All sources are declared in `sources.tex` before the document body. Declare them
in alphabetical order within each section.

### Case Law

```latex
\declarecase{key}
  {Full Case Name}
  {Year Court Docket}
  {Short}
```

Example:

```latex
\declarecase{vavilov}
  {Canada (Minister of Citizenship and Immigration) v Vavilov}
  {2019 SCC 65}
  {Vavilov}
```

The short form is automatically italicised in footnotes and running text.

### Legislation

```latex
\declarelegislation{key}
  {Full Act Title}
  {Statute Citation}
```

Example:

```latex
\declarelegislation{copyrightact}
  {Copyright Act}
  {RSC 1985, c C-42}
```

### Monographs

```latex
\declarebook{key}
  {Footnote Author}
  {Bibliography Author}
  {Title}
  {Edition}
  {Publisher}
  {Year}
  {Short}
```

### Journal Articles

```latex
\declarearticle{key}
  {Footnote Author}
  {Bibliography Author}
  {Title}
  {Year}
  {Vol:Issue}
  {Journal}
  [FirstPage]
  {Short}
```

## Citing in `body.tex`

| Command | Output |
|---------|--------|
| `\legal{key}` | Footnote: full citation `[Short]` on first use |
| `\legal[pinpoint]{key}` | Footnote with pinpoint |
| `\legal{key}` repeated consecutively | `Ibid` |
| `\legal[pinpoint]{key}` repeated consecutively | `Ibid` with pinpoint |
| `\legal{key}` repeated later | Short form |
| `\legalname{key}` | Source name in running text |
| `\legalshort{key}` | Short form in running text |

### Pinpoint Syntax

| Source type | Examples |
|-------------|----------|
| Cases | `para 32` · `paras 27-31` · `paras 18, 23` |
| Books | `p 42` · `pp 148-155` · `pp 214, 218` |
| Articles | `p 5` · `pp 5-7` |

## Table of Authorities

Place `\printlegalbibliography` at the end of `main.tex`. It prints a formatted
table of authorities divided into legislation, case law, monographs, and articles.
