
## 16. Typesetting and Word Processing

If you're coming to Linux with a Microsoft Windows or Apple MacOS background, or from some other non-Unix computing environment, you are likely used to one approach to "word processing." In these environments, most writing is done in word processors—large programs that offer a vast array of formatting options and that store their output in proprietary file formats. Most people use word processors no matter where the intended output will go (even if it's just your diary).

Word processors, from complete suites like StarOffice to commercial favorites like WordPerfect, are available for Linux—and have been for years. However, the standard personal-computing paradigm known as "word processing" has never really taken off on Linux—or, for that matter, on Unix-like operating systems in general. With Linux, most writing is done in a text editor, and files are kept in plain text.

When you keep a file in plain text, you can use command-line tools to format the pages and paragraphs; add page numbers and headers; check the spelling, style, and usage; count the lines, words, and characters it contains; convert it to HTML and other formats; and even print the text in a font of your choosing—all of which are described in the recipes in this book. The text can be formatted, analyzed, cut, chopped, sliced, diced, and otherwise processed by the vast array of Linux command-line tools that work on text—over 750 in an average installation.

This approach may seem primitive at first—especially to those weaned in a computing environment that dictates that all writing must be set in a typeface from the moment of creation—but the word-processing approach can be excessive compared to what Linux provides. You can, if you like, view or print plain text in a font, with a single command—which is what ninety percent of people want to do with a word processor ninety percent of the time, anyway; to do this, see Converting Plain Text for Output.

It's my opinion that word processing is not a forward-thinking direction for the handling of text, especially on Linux systems and especially now that text is not always destined for printed output: text can end up on a Web page, in an "eBook," (25) in an email message, or possibly in print. The best common source for these formats is plain text. Word processing programs, and the special file formats they require, are anathema to the generalized, tools-based and plain-text philosophy of Unix and Linux (see section Unix and the Tools Philosophy). "Word processing" itself may be an obsolete idea of the 1980s personal computing environment, and it may no longer be a necessity in the age of the Web and email—mediums in which plain text content is more native than proprietary word processor formats.

If you do need to design a special layout for hardcopy, you can typeset the text. One could write a book on the subject of Linux typesetting; unfortunately, no such book has yet been written, but this chapter contains recipes for producing typeset text. They were selected as being the easiest to prepare or most effective for their purpose.

NOTE: For more information on this subject, I recommend Christopher B. Browne's excellent overview, "Word Processors for Linux".

- 16.1 Choosing the Right Typesetting System for the Job
  Choosing the typesetting system to use.
- 16.2 Converting Plain Text for Output
  Converting plain text to PostScript.
- 16.3 LyX Document Processing
  LyX, a document processor.
- 16.4 Typesetting with TeX and Friends
  TeX and friends.
- 16.5 Writing Documents with SGMLtools
  SGML and markup language.
- 16.6 Other Word Processors and Typesetting Systems
  Other typesetting systems.

### 16.1 Choosing the Right Typesetting System for the Job

Choosing the proper typesetting system to use when you are about to begin a project can be daunting: each has its own drawbacks and abilities, and to the less experienced it may not be immediately clear which is most appropriate for a particular document or project.

The following table can help you determine which system is best for a particular task. There isn't one way of doing such things, of course---these are only my recommendations. The first column lists the kind of output you intend, the second gives examples of the kind of documents, and the third suggests the typesetting system(s) to use. These systems are described in the remaining sections of this chapter.

| INTENDED OUTPUT | EXAMPLES | TYPESETTING SYSTEM |
|---|---|---|
| Printed, typeset output and electronic HTML or text file | Internet FAQ, white paper, dissertation | enscript; Texinfo; SGMLtools |
| Printed, typeset output and text file | man page, command reference card | groff |
| Printed, typeset output | Letter or other correspondence, report, book manuscript | LaTeX or LyX |
| Printed, typeset output | Brochure or newsletter with multiple columns and images | LyX |
| Printed, typeset output | Envelope, mailing label, other specialized document | TeX |
| Printed text output in a font | Grocery list, saved email message, to-do list | enscript |
| Printed, typeset output | Poster, sign | enscript; HTML; LyX; TeX |
| Large printed text output | Long banners for parties or other occasions | banner |

NOTE: If you really don't need a document to be typeset, then don't bother! Just keep it a plain text file, and use a text editor to edit it (see section Text Editing). Do this for writing notes, email messages, Web pages, Usenet articles, and so forth. If you ever do need to typeset it later, you will still be able to do so. And you can, if you like, view or print plain text in nice fonts (see section Outputting Text in a Font).
