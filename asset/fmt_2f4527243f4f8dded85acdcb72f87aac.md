
```latex
\documentclass{article}

\begin{document}

\Huge

Today, \today, I formally declare my candidacy for the

position of \itshape{towncatcher}.

\end{document}
```

为了完全掌握 `LaTeX`，你必须投入精力学习它的复杂性。如果你编写典型的文档并已经熟悉 `GUI` 方法，那么这种努力可能不值得；但如果你需要 `LaTeX` 的强大功能，你可能想买一本相关的书籍，或者查看 `http://www.latex-project.org` 上的文档。

如果你将列表 7.1 或其他 `LaTeX` 文档输入文件，你可以通过 `latex` 程序将其转换为其他格式。该程序将 `LaTeX` 文档（通常使用 `.tex` 文件名）转换为设备无关（`DVI`）文件，这实际上是一种中间格式。为了产生用的输出文件，你会使用 `dvips` 或 `dvipdf` 程序，分别创建便携文档格式（`PDF`）文件。其他转换程序也可以将其转换为其他格式。在创建 `announce.tex` 后，你可能使用这些命令创建 `PDF`：

```bash
$ latex announce.tex
$ dvipdf announce.dvi
```
