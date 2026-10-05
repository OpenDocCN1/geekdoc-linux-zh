# WORKING TECHNIQUES 639

+   * PAGESTYLE specifies the layout of headers and footers.
* SIDES specifies whether the position of section and page number is inverted on every second page (for a two-sided layout as in this book).
* COLUMNS specifies the number of columns. In two-column text, the columns are simply filled one after the other. This layout is not visible in LaTeX itself.
* FONTS specifies the default font. With default, LaTeX fonts are used; with Times, Palainno, and so on. PostScript fonts are used instead (This book, for example, is in Times.).
* FONT SIZE specifies the size of the default font in the range between 10 and 12 points. All other font sizes (for titles, and so on) are modified accordingly.
* LANGUAGE specifies the language to be used for the hyphenation rules and for predefined text elements (such as Figure/Abbildung in figure captions).
* SEPARATION specifies whether paragraphs are to be separated by a first line indent (default, also used in this book) or by vertical spacing.
* DEFAULT SKIP specifies the vertical distance between two paragraphs.
* SPACING specifies the line spacing inside a paragraph.
* FLOAT PLACEMENT specifies where movable elements (tables, figures) should be preferably placed. Legal settings are t (top), h (here), and b (bottom).

![](bbox=[0.303, 0.473, 0.763, 0.737])

**Figure 19.4** Document layout dialog.

> During a later change of document class, information on the required paragraph format is lost if this format does not exist in the new document class (for example chapter in a letter). At the beginning of such paragraphs, an ‘error’ box indicates the problem. This box must be deleted and a new format selected for the paragraph. The change of document class cannot be undone.