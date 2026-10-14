⇒ To ensure that all of the cross references in lshort.tex have been generated properly, run the input file through latex once more:
$ latex lshort.tex [RET]

The lshort.dvi file will be rewritten with an updated version containing the proper page numbers in the cross reference and index entries. You can then view, print, or convert this DVI file as described in the previous recipe for processing TeX files.

# 15.3.4 Getting Started with TeX and LaTeX

To create a document with TeX or LaTeX, you generally use your favorite text editor to write an input file containing the text in TeX or LaTeX formatting. Then, you process this TeX or LaTeX input file to create an output file in the DVI format, which you can preview, convert, or print.

It’s an old tradition among programmers introducing a programming language to give a simple program that just outputs the text “Hello, world” to the screen; such a program is usually just detailed enough to give those unfamiliar with the language a feel for its basic syntax.

We can do the same with document-processing languages like TeX and LaTeX. Figure 15-1 contains the “Hello, world” for a TeX document.

```
Hello, world
\end
```

Figure 15-1. A TeX “Hello, world.”

If you processed the input file shown in Figure 15-1 with tex, it would output a DVI file that displayed the text “Hello, world” in the default TeX font, on a default page size, and with default margins.

Figure 15-2 contains the same “Hello, world,” but for LaTeX.

```
\documentclass{article}
\begin{document}
Hello, world
\end{document}
```

Figure 15-2. A LaTeX “Hello, world.”

Even though the TeX example in Figure 15-1 is much simpler than the LaTeX example, LaTeX is generally easier to use “fresh out of the box” for