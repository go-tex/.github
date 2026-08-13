<p align="center"><img src="https://raw.githubusercontent.com/go-tex/brand/main/social/go-tex.png" alt="go-tex" width="720"></p>

<h1 align="center">go-tex</h1>

<p align="center"><strong>Pure-Go TeX that runs the real LaTeX classes — in Go and in the browser.</strong></p>

<p align="center">
<img src="https://img.shields.io/badge/license-BSD--3--Clause-blue" alt="BSD-3-Clause">
<img src="https://img.shields.io/badge/cgo-disabled-1a7f37" alt="CGO=0">
<img src="https://img.shields.io/badge/go-1.26.4%2B-00ADD8" alt="Go 1.26.4+">
<img src="https://img.shields.io/badge/js%2Fwasm-ready-8A2BE2" alt="js/wasm ready">
</p>

`go-tex` is a pure-Go (`CGO_ENABLED=0`) TeX effort. Its engine is a faithful
re-implementation of TeX — the category-code mouth and gullet, a scaled-point
stomach, math, fonts, and PDF/SVG output — and on top of it, it **loads and runs
the genuine LaTeX classes**: `\documentclass{article}`, `{report}` and `{book}`
execute the real, embedded `.cls` files (LPPL, verbatim) — not an emulation — in
native builds **and** in the browser via `js/wasm`, with no TeXLive and no
server.

## What it does

- **Runs the standard base classes for real.** `article`, `report` and `book`
  load and execute the genuine LaTeX `.cls` files, typesetting a numbered title,
  a dotted `\tableofcontents`, numbered sections/subsections, `\chapter`
  (report/book), numbered figure/table captions, `itemize`/`enumerate`, and math.
- **A full pipeline.** A category-code mouth and gullet, a scaled-point stomach
  with Knuth–Plass line breaking and a cost-based page builder, `\halign` tables,
  math via [`go-tex/math`](https://github.com/go-tex/math) (vector output),
  OpenType fonts (a built-in default font, kerning, ligatures), and **PDF + SVG**
  output — the SVG carries a source map for click-to-line.
- **In the browser.** Genuine LaTeX class rendering client-side via `js/wasm` —
  no TeXLive, no server (a self-contained WASM demo ships with the engine).
- **Gated by objective oracles.** A byte-exact **conformance ratchet**
  (`TestConformance`) and a **whole-document prose fidelity check against a real
  LaTeX engine** (`tectonic`). On a sample of real arXiv `article` papers, the
  real class reproduces about **90% (median)** of the reference engine's prose
  words.
- **Portable and clean.** `CGO_ENABLED=0`, `go vet` clean, CI green across three
  64-bit arches under QEMU (`riscv64`/`ppc64le`/`s390x`) plus macOS, Linux and
  Windows, and both `js/wasm` and `wasip1/wasm`.

## Repositories

- [**engine**](https://github.com/go-tex/engine) — the pure-Go TeX engine:
  faithful mouth + gullet, scaled-point stomach, math, OpenType fonts, PDF/SVG,
  and the real LaTeX base classes (`article`/`report`/`book`), native and
  `js/wasm`.
- [**math**](https://github.com/go-tex/math) — pure-Go TeX math-mode typesetter
  (fractions, radicals, matrices, big operators, in-math font switches, named
  operators, `\operatorname`, `\bmod`/`\pmod`, long arrows) → vector output.
- [**tex**](https://github.com/go-tex/tex) — a lightweight LaTeX-subset document
  processor → semantic HTML (macro expansion + structure + math), `js/wasm`-ready.
- [**brand**](https://github.com/go-tex/brand) — logos & icons.
- [**docs**](https://go-tex.github.io/docs/) · [landing](https://go-tex.github.io/)

## Scope — honest limits

The engine **loads and runs the standard base classes**; it is
functional-parity-oriented and held to real-LaTeX fidelity, **not** a claim of
full TeXLive parity. `amsart` and heavy packages (`tikz`, `hyperref`, …) are not
yet run as real files — that is the roadmap, not done.

## Conventions

Every module is `CGO_ENABLED=0` and standard-library-first, BSD-3-Clause
licensed, with a ratcheted conformance gate in CI.
