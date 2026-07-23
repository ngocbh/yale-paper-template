# Building the paper

The paper source is **`main.tex`** (class `yalearxiv.cls`, bibliography
`main.bib`). Building it produces **`main.pdf`**.

## Environment

Uses the local **TinyTeX** install (TeX Live 2026) — no system TeX needed:

```
$HOME/.TinyTeX/bin/x86_64-linux/    # latexmk, pdflatex, bibtex live here
```

Put it on `PATH` before building:

```bash
export PATH="$HOME/.TinyTeX/bin/x86_64-linux:$PATH"
```

## Compile

Run from this directory (`docs/paper/`):

```bash
export PATH="$HOME/.TinyTeX/bin/x86_64-linux:$PATH"
unset http_proxy https_proxy HTTP_PROXY HTTPS_PROXY   # sandbox has a dead proxy
latexmk -pdf -interaction=nonstopmode main.tex
```

`latexmk` runs the full `pdflatex → bibtex → pdflatex → pdflatex` cycle
automatically, so citations and cross-references resolve in one command.
Output: `main.pdf`.

## Clean build artifacts

```bash
export PATH="$HOME/.TinyTeX/bin/x86_64-linux:$PATH"
latexmk -C main.tex        # removes .aux/.bbl/.log/... and the PDF
```

Use `latexmk -c` instead to keep the PDF and drop only the intermediates.

## Checking a build succeeded

```bash
grep "Output written" main.log | tail -1                     # page count
grep -i "Citation.*undefined\|Reference.*undefined" main.log # should be empty
```

## Notes

- If `pdflatex` cannot be found, the `PATH` export above was skipped.
- If a build hangs on a download/network step, confirm the proxy vars are unset.
