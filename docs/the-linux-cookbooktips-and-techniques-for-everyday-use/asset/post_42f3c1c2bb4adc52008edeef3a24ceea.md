
## 16.3 LyX Document Processing

```
@sf{Debian:}`lyx'
@sf{WWW}: http://www.lyx.org/
```

LyX is a relative newcomer to the typesetting and word-processing arena, and it is one of the most genuinely fresh ideas in the field: it's a kind of word processor for writing LaTeX input (see section Typesetting with TeX and Friends). It's a visual, graphic editor for X, but it doesn't emulate the output paper directly on the display screen. In contrast to specifying exactly how each character in the document will look ("make this word Helvetica Bold at 18 points"), you specify the structure of the text you write ("make this word a chapter heading"). And, in contrast to the WYSIWYG paradigm, its authors call the new approach WYSIWYM—"What you see is what you mean."

LyX comes with many document classes already defined—such as letter, article, report, and book—containing definitions for the elements these document types may contain. You can change the look of each element and the look of the document as a whole, and you can change the look of individual selections of text, but with these elements available, it's rarely necessary.

Since LyX uses LaTeX as a back-end to do the actual typesetting, and LyX is capable of exporting documents to LaTeX input format, you can think of it as a way to write LaTeX input files in a GUI without having to know the LaTeX language commands.

However, even those who do use LaTeX and related typesetting languages can get some use out of LyX: many people find it quick and easy to create some documents in LyX that are much harder to do in LaTeX, such as multi-column newsletter layouts with illustrations.

(One excellent example of this is http://www.bcgs.org/newsletters/bcgs_newsletter-2000-01.pdf)

You can also import your LaTeX files (and plain text) into LyX for further layout or manipulation.

The following recipes show how to get started using LyX, and where to go to learn more about it.

### 16.3.1 Features of LyX

When editing in LyX, you'll see that it has all of the commands you'd expect from a word processor—for example, some of the commands found on the Edit menu include Cut, Copy, Paste, Find and Replace, and Spell Check.

Here are some of its major features:

- Automatic generation of table of contents, nested lists, and numbering of section headings.
- Easy insertion of PostScript figures and illustrations, which can be rotated, scaled, and captioned.
- WYSIWYG construction of tables.
- Undo and redo of any operation or sequence of operations.
- All LyX functions available from both keyboard commands and pull-down menus.
- All key-presses used for commands are configurable.

### 16.3.2 Writing Documents with LyX

LyX runs under X, and you start it in the usual way—either by choosing it from the applications menu provided by your window manager or by typing lyx in an xterm window. (For more about starting programs in X, see section Running a Program in X).

To start a new document from scratch, choose New from the File menu. You can also make a document from one of the many templates included with LyX, which have the basic layout and settings for a particular kind of document all set up for you—just fill in the elements for your actual document. To make a new document from a template, choose New from template from the File menu, and then select the name of the template to use.

The following table lists the names of some of the included templates and the kind of documents they're usually used for:

| TEMPLATE FILE | DOCUMENT FORMAT |
| aapaper.lyx | Format suitable for papers submitted to *Astronomy and Astrophysics.* |
| dinbrief.lyx | Format for letters typeset according to German conventions. |
| docbook_template.lyx | Format for documents written in the SGML DocBook DTD. |
| hollywood.lyx | Format for movie scripts as they are formatted in the U.S. film industry. |
| iletter.lyx | Format for letters typeset according to Italian conventions. |
| latex8.lyx | Format suitable for article submissions to IEEE conferences. |
| letter.lyx | Basic format for letters and correspondence. |
| linuxdoctemplate.lyx | Format for documents written in the SGML LinuxDoc DTD, as formerly used by the Linux Documentation Project. |
| revtex.lyx | Article format suitable for submission to publications of the American Physical Society (APS), American Institute of Physics (AIP), and Optical Society of America (OSA). |
| slides.lyx | Format for producing slides and transparencies. |

To view how the document will look when you print it, choose View DVI from the File menu. This command starts the xdvi tool, which previews the output on the screen. (For more on using xdvi, see section Previewing a DVI File).

To print the document, choose Print from the File menu. You can also export it to LaTeX, PostScript, DVI, or plain text formats; to do this, choose Export from the File menu and then select the format to export to.

> *NOTE:* If you plan on editing the document again in LyX, be sure to save the actual `.lyx` document file.

### 16.3.3 Learning More about LyX

The LyX Documentation Project has overseen the creation of a great deal of free documentation for LyX, including hands-on tutorials, user manuals, and example documents.

The LyX Graphical Tour is a Web-based tutorial that shows you how to create and edit a simple LyX file.

LyX has a comprehensive set of built-in manuals, which you can read inside the LyX editor like any LyX document, or you can print them out. All of the manuals are available from the Help menu.

- To run LyX's built-in tutorial, choose Tutorial from the Help menu.

This command opens the LyX tutorial, which you can then read on the screen or print out by selecting Print from the File menu.
