
To write a document with a template, insert the contents of the template file into a new file that has a .tex or .ltx extension, and write your document by making changes to that file. (Use your favorite text editor to do this.)

To make sure that you don't accidentally overwrite the actual template files, you can write-protect them (see Recipe 6.3.3 [Write-Protecting a File], page 169):

```
$ chmod a-w template-file-names RET
```

In the templates themselves, the bracketed, uppercase text explains what kind of text belongs there; fill in these lines with your own text and delete the lines you don't need. Then, process your new file with either latex or tex as appropriate, and you've got a great-looking document!

The following table lists the file names of the TeX templates, and describes their use. Use tex to process files you make with these templates (see the preceding recipe).

| fax.tex | A cover sheet for sending fax messages. |
| envelope.tex | A No. 10 mailing envelope. |
| label.tex | A single mailing label for printing on standard 15-up sheets. |

The following table lists the file names of the LaTeX templates, and describes their use.⁶ Use latex to process files you make with these templates (see Recipe 15.3.3 [Processing a LaTeX File], page 374).

| letter.ltx | A letter or other correspondence. |
| article.ltx | An article or a research or term paper. |
| manuscript.ltx | A book manuscript. |

There are more complex template packages available on the net that you might want to look at:

- The largest listing of LaTeX and TeX templates and style files (and other related software and documentation) on the Internet is the searchable TeX Catalogue Online [http://www.ctan.org/tex-archive/help/Catalogue/hier.html].

⁶ The manuscript template requires that your system has the LaTeX style file called manuscript.sty; most TeX distributions have this installed at /usr/share/texmf/tex/latex/misc/manuscript.sty.

documents in LyX that are much harder to do in LaTeX, such as multi-column newsletter layouts with illustrations.

You can also import your LaTeX files (and plain text) into LyX for further layout or manipulation.

The following recipes show how to get started using LyX, and where to go to learn more about it.

When editing in LyX, you'll see that it has all of the commands you'd expect from a word processor—for example, some of the commands found on the Edit menu include Cut, Copy, Paste, Find and Replace, and Spell Check.

Here are some of its major features:

- Automatic generation of table of contents, nested lists, and numbering of section headings.
- Easy insertion of PostScript figures and illustrations, which can be rotated, scaled, and captioned.
- WYSIWYG construction of tables.
- Ability to undo and redo any operation or sequence of operations.
- All LyX functions available from both keyboard commands and pull-down menus.
- All keypresses used for commands are configurable.

## 15.4.1 Getting Started with LyX

LyX runs under X, and you start it in the usual way—either by choosing it from the applications menu provided by your window manager, or by typing lyx in an xterm window. (For more about starting programs in X, see Recipe 4.2 [Running a Program in X], page 101).

To start a new document from scratch, choose New from the File menu. You can also make a document from one of the many templates included with LyX, which have the basic layout and settings for particular kind of documents all set up for you—just fill in the elements for your actual document. To make a new document from a template, choose New from template from the File menu, and then select the name of the template to use.

The following table lists the names of some of the included templates and the kind of documents they're usually used for.

| aapaper.lyx | Format suitable for papers submitted to *Astronomy and Astrophysics*. |
| dinbrief.lyx | Format for letters typeset according to German conventions. |
| docbook_template.lyx | Format for documents written in the SGML DocBook DTD. |
| hollywood.lyx | Format for movie scripts as they are formatted in the U.S. film industry. |
| iletter.lyx | Format for letters typeset according to Italian conventions. |
| latex8.lyx | Format suitable for article submissions to IEEE conferences. |
| letter.lyx | Basic format for letters and correspondence. |
| linuxdoctemplate.lyx | Format for documents written in the SGML LinuxDoc DTD, as formerly used by the Linux Documentation Project. |
| revtex.lyx | Article format suitable for submission to publications of the American Physical Society (APS), American Institute of Physics (AIP), and Optical Society of America (OSA). |
| slides.lyx | Format for producing slides and transparencies. |

To view how the document will look when you print it, choose View DVI from the File menu. This command starts the xdvi tool, which previews the output on the screen. (For more on using xdvi, see Recipe 17.4.1 [Previewing a DVI File], page 413).

To print the document, choose Print from the File menu. You can also export it to LaTeX, PostScript, DVI, or plain text formats; to do this, choose Export from the File menu and then select the format to export to.

**NOTES:** If you plan on editing the document again in LyX, be sure to save the actual .lyx document file.
