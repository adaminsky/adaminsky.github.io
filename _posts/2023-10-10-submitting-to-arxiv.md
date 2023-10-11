---
layout: post
title:  "Submitting to arXiv"
categories: info research
---

After submitting my first paper to arXiv, I realized this is not an easy
process, especially if you don't want to accidentally share all your comments
and work-in-progress figures. To help others and my future self, I'm documenting
the process to use for the next time. These steps will condense a latex project
into a single .tex file, remove all comments, remove unused figures, and prepare
a tar file for submission.

1. Install `arxiv_latex_cleaner` by running the following:
```bash
pip install arxiv-latex-cleaner
```
2. Run `arxiv_latex_cleaner —-keep_bib <directory>` where directory is replaced
   with the path the the latex source code. This removes all unused figures.
3. Run `latexpand -—empty-comments arxiv.tex > arxiv_main.tex` to remove all
   comments and make all latex files into one file. The file "arxiv.tex" should
   be replaced with the name of the main tex file in the project.
4. Build the latex code by running the following sequence of commands:
```bash
pdflatex arxiv_main
biber arxiv_main # alternatively replace biber with bibtex if this doesn't work
pdflatex arxiv_main
pdflatex arxiv_main
```
This will generate a lot of output files. Check that arxiv_main.pdf looks
correct and delete all produced files except for the .bbl file.
5. Create a tar with `tar czvf arxiv.tar.gz ./*`
6. Submit to arXiv at exactly 1:59pm.
