# 16.4.4 Writing Documents with TeX and LaTeX

@ssf (WWW): ftp://ctan.tug.org/tex-archive/documentation/gentle.tex
@ssf (WWW): ftp://ctan.tug.org/tex-archive/documentation/lshort/

To create a document with TeX or LaTeX, you generally use your favorite text editor to write an input file containing the text in TeX or LaTeX formatting. Then, you process this TeX or LaTeX input file to create an output file in the DVI format, which you can preview, convert, or print.

It's an old tradition among programmers introducing a programming language to give a simple program that just outputs the text `Hello, world' to the screen; such a program is usually just detailed enough to give those unfamiliar with the language a feel for its basic syntax.

We can do the same with document processing languages like TeX and LaTeX. Here's the "Hello, world" for a TeX document:

```
Hello, world
\end
```

If you processed this input file with tex, it would output a DVI file that displayed the text `Hello, world' in the default TeX font, on a default page size, and with default margins.

Here's the same "Hello, world" for LaTeX:

```
\documentclass{article}
\begin{document}
Hello, world
\end{document}
```

Even though the TeX example is much simpler, LaTeX is generally easier to use fresh "out of the box" for writing certain kinds of structured documents—such as correspondence and articles—because it comes with predefined document classes which control the markup for the structural elements the document contains(27). Plain TeX, on the other hand, is better suited for more experimental layouts or specialized documents.

The TeX and LaTeX markup languages are worth a book each, and providing an introduction to their use is well out of the scope of this text. To learn how to write input for them, I suggest two excellent tutorials, Michael Doob's A Gentle Introduction to TeX, and Tobias Oetiker's The Not So Short Introduction to LaTeX—each available on the WWW at the URLs listed above. These files are each in the respective format they describe; in order to read them, you must process these files first, as described in the two previous recipes.

Good LaTeX documentation in HTML format can be found installed on many Linux systems in the `/usr/share/texmf/doc/latex/latex2e-html/` directory; use the lynx browser to view it (see section Browsing Files).

Some other typesetting systems, such as LyX, SGMLtools, and Texinfo (all described elsewhere in this