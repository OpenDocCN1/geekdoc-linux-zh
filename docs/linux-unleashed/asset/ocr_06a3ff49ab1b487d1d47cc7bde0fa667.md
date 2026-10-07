You can also vary page styles in your document using the \thispagestyle command. This applies the supplied page style to the current page only.

# ## Using Special Characters

LaTeX supports the use of international characters, such as umlauts ('') and circumflexes (^). These characters are generated using a command variant on the letter itself. For example, the text

```
```
What a na\"i ve fj\o rd you are!
```
```

produces the following:

```
```
What a naïve fjörd you are!
```
```

International spacing can also be applied using the \frenchspacing command. This command tells LaTeX not to insert the usual extra space after a period.

# ## Putting Structure into a LaTeX Document

LaTeX has commands that make it easy to enhance your document structurally, thus making it easier for the reader to digest. For the *article* document class, the commands are as follows:

+   - \section
- \subsection
- \subsubsection
- \paragraph
- \subparagraph, and
- \appendix.

These commands, with the exception of \appendix, accept titles as arguments, and are declared before the body of text that they represent. LaTeX takes care of the rest; it sets the appropriate spacing between sections, section numbering, and title font. The \appendix command uses alphabetic increments in order to number succeeding appendix sections.

For the *report* and *book* classes, there are two additional commands: \part and \chapter. The \part command enables you to insert a section without affecting the