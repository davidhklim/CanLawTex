# CanLawTex

A LaTeX template for Canadian legal writing that implements footnote-based citations
following the **Canadian Guide to Uniform Legal Citation (McGill Guide, 9th ed.)**.

## Files

| File | Purpose |
|------|---------|
| `legalcite.sty` | Citation package — do not edit unless extending functionality |
| `main.tex` | Document shell: packages, title, abstract, bibliography |
| `sources.tex` | All source declarations (edit here to add/change sources) |
| `body.tex` | Paper body — **write your paper here** |

## Quick Start

1. Open `sources.tex` and declare your sources (see [Declaring Sources](#declaring-sources)).
2. Open `body.tex` and write your paper using `\legal{}`, `\legalname{}`, and `\legalshort{}`.
3. Compile with `pdflatex` twice:
   ```
   pdflatex main.tex
   pdflatex main.tex
   ```

## Declaring Sources

All sources are declared in `sources.tex` **before** the document body.
Declare them in **alphabetical order** within each section (required by McGill Guide §1.4).

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

> The short form is automatically italicised in footnotes and running text (McGill Guide §3.5).

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

### Monographs (Books)

```latex
\declarebook{key}
  {Footnote Author}       % e.g., "B. Ziff"
  {Bibliography Author}   % surname-first, e.g., "Ziff, B."
  {Title}
  {Edition}               % e.g., "5th ed" — use {} for a first edition
  {Publisher}
  {Year}
  {Short}
```

Example:
```latex
\declarebook{ziff}
  {B. Ziff}
  {Ziff, B.}
  {Principles of Property Law}
  {5th ed}
  {Carswell}
  {2010}
  {Ziff}
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
  [FirstPage]             % optional, but required by McGill Guide §6.1
  {Short}
```

Example:
```latex
\declarearticle{debeer}
  {J. de Beer}
  {de Beer, J.}
  {Canada's Copyright Tariff-Setting Process: An Empirical Review}
  {2016}
  {63:3}
  {Journal of the Copyright Society of the U.S.A.}
  [399]
  {de Beer}
```

## Citing in the Body (`body.tex`)

| Command | Output |
|---------|--------|
| `\legal{key}` | Footnote: full citation `[Short]` (first use) |
| `\legal[pinpoint]{key}` | Footnote: full citation `at pinpoint [Short]` (first use) |
| `\legal{key}` (repeat, consecutive) | Footnote: *Ibid* |
| `\legal[pinpoint]{key}` (repeat, consecutive) | Footnote: *Ibid* at pinpoint |
| `\legal{key}` (repeat, non-consecutive) | Footnote: Short form |
| `\legalname{key}` | Source name in running text (no footnote) |
| `\legalshort{key}` | Short form in running text (no footnote) |

### Pinpoint Syntax (McGill Guide §1.3)

| Source type | Examples |
|-------------|---------|
| Cases | `para 32` · `paras 27-31` · `paras 18, 23` |
| Books | `p 42` · `pp 148-155` · `pp 214, 218` |
| Articles | `p 5` · `pp 5-7` |

### Example

```latex
The SCC ruled in \legalname{vavilov}\legal{vavilov} that reasonableness
is the presumptive standard of review.
The Court confirmed this position.\legal[para 10]{vavilov}
See also \legalshort{socan}.\legal[para 28]{socan}
```

## Table of Authorities

Place `\printlegalbibliography` at the end of `main.tex` (already included in the
template). It prints a formatted **Table of Authorities** divided into:

- Legislation
- Case Law
- Secondary Sources
  - Monographs
  - Articles

Sources appear in the order they were declared in `sources.tex` — declare them
alphabetically within each section to comply with McGill Guide requirements.

## Requirements

- A standard TeX distribution (TeX Live, MiKTeX, or MacTeX)
- Packages: `xparse`, `etoolbox` (both included in standard distributions)
