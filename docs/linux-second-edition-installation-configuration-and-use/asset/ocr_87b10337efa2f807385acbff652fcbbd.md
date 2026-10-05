# 604 LATEX

```
\{\smverb?}
\ fixed space (for example in (\smverb?5cm))\
{\smverb?)}
\ includes text areas (for example, for special formatting)\n{\smverb?formula}$\n\ includes formulae in flow text\
{\smverb_?}
\ subscript (only in mathematical mode)\n{\smverb?}
\ superscript (only in mathematical mode)\n\end{tabbing}
```

If this simple table format is not sufficient for you, \LaTeX provides the tabular environment which can be used to create tables with varying column width, frames, and so on. If in addition you also use the table environment, the is automatically placed in the same way as an illustration. using the available space without creating gaps in the text.

![](bbox=[0.268, 0.292, 0.313, 0.355])

# Bulleted and numbered lists

\LaTeX offers several possibilities for formatting lists of items. The simplest variation is constituted by the itemize environment.

# Lists

```
\begin{itemize}
\item Text of the first item
\item Second item
\end{itemize}
```

The following example shows the visual layout of a bulleted list:
\begin{itemize}
\item \LaTeX marks the items of a List with thick black bullets (special character \verb?$?).
\item At the same time the entries are indented with respect to the normal text.
\end{itemize}

+   * \LaTeX marks the simple items of a list with thick black bullets ($$).

+   * At the same time the entries are indented with respect to the normal text.

If instead of itemize use the environment name enumerate, \LaTeX uses numbers (1., 2., and so on). Both environments can be embedded into each other. Depending on the level of embedding, different symbols are used for the bullets and different kinds of numbers for enumeration (lower case letters, roman numbers, and so on). In addition, the list items are indented by different amounts of space.