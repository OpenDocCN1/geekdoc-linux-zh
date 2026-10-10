
claim that OQXMI is so specific in requiring support for Microsoft product features, without providing any guidance on how those Microsoft proprietary features can be implemented, that it is unusable as a standard. In other words, don't think that, because Microsoft is claiming to support standards, you will ever be able to fully use Microsoft document formats on other platforms.

To open OpenOffice.org Writer, Impress, Calc, and other office applications, click Office from the Applications menu. Then select the OpenOffice.org application you want to open. Figure 6-1 shows an example of OpenOffice.org.

## FIGURE 6-1

Work with documents in OpenOffice.org Writer.

![](img/2f265415ceec72538dd3c78ffca75c10_257_0.png)

The controls in OpenOffice.org are similar to the ones you would find in Word prior to Word 2007. So if you were comfortable with those controls, you should find it easy to transition to OpenOffice.org Writer. In fact, you might find it easier than using Microsoft Word 2007, since many people have found the transition to Word 2007 difficult.

Toolbars in OpenOffice.org Writer include boxes for identifying filenames and changing styles, font types, and font sizes. Buttons enable you to save and print the file, change the text alignment, and cut, copy, and paste text. In other words, Writer includes almost everything you expect in an advanced word processor. In addition, Writer includes a handy PDF button to output a file directly to the PDF format. This is very useful for exchanging documents or placing data on the Internet.

If you are just starting out with OpenOffice.org Writer, here are a few features you can try out:

- **Wizards** — Use a wizard to start a letter, fax, agenda, presentation, web page, Document Converter, or Euro Converter. Select File > Wizards and then choose one of the document types just mentioned. The Document Converter Wizard lets you convert a directory of Microsoft or StarOffice documents to OpenDocument format. The Euro Converter lets you convert files containing different European currencies to Euros.
- **Document Styles and Formatting** — Create the format of your documents using character, paragraph, frame, page, and numbering styles (select Format > Styles and Formatting). From the Styles and Formatting window, choose the type of style you want to change, right-click in the Styles box, and choose New to create your own style.
- **Checking Documents** — Try different features for checking and correcting your documents. Writer includes features such as spell checking (Tools > Spelling and Grammar) and autocorrection (Tools > AutoCorrect). You can display the content as a web page or in print layout and view font and character markup (View > Nonprinting Characters).
- **Drawing and Images** — Use drawing tools (View > Toolbars > Drawing) to create drawings, flow charts, callouts, or symbols in your documents. Insert background colors or graphics on your pages (Format > Page, select Background tab, and choose color or graphic). To insert a graphic, select Insert > Picture, and insert the image from a file or from your scanner.
- **Outputting PDF or Other Formats** — Writer provides a toolbar button that will output your current document to PDF format. PDF is a good format for sharing documents that you want others to read or print, but don’t necessarily want to give them the original source file. You can also save Writer documents to other useful formats, including HTML (to publish your document to the Web) or Rich Text Format (to be able to share the document with different word processors).

> **NOTE** Find out more about OpenOffice.org at www.OpenOffice.org.

### Other Word Processors

As for commercial offerings, there is StarOffice from Sun Microsystems and TextMaker.

### StarOffice

The StarOffice productivity suite (www.sun.com/staroffice) from Sun Microsystems, Inc is a commercial product that runs on Linux, UNIX, and Windows operating systems. StarOffice contains applications for word processing, spreadsheets, presentation graphics, e-mail, news, charting, and graphics. Like OpenOffice.org, StarOffice contains many features that make it compatible with Microsoft Office applications. In particular, it includes the capability to import Microsoft Word and Excel files.

# Part II Using CentOS

StarOffice is probably the most complete integrated office suite for Linux. If you are working in a cross-platform environment, however, you can also get StarOffice for Sun Solaris and Microsoft Windows operating systems. StarOffice includes:

- **StarOffice Writer** — This is the StarOffice word processing application. It can import documents from a variety of formats, with special emphasis on Word documents.
- **StarOffice Calc** — This is the spreadsheet program that comes with StarOffice. You can import spreadsheets from Microsoft Excel and other popular programs.
- **StarOffice Impress** — This module enables you to create presentations.
- **StarOffice Draw** — This is a vector-oriented drawing program. It includes the capability to create 3D objects and to use texturing.
- **StarOffice Base** — You can manage your data with StarBase, a friendly front-end for databases. It can access a variety of database interfaces.

There are also other tools in StarOffice that enable you to create business graphics, edit raster images, and edit mathematical formulas (StarOffice Math).

You can download StarOffice 9 for Linux or purchase a boxed set from the StarOffice web site at `www.sun.com/software/star/staroffice`.

Although StarOffice was once available free for download, the current price (at time of writing) to download the software for home users is $34.95.

### TextMaker

TextMaker is another popular commercial word processing package for Linux (www.softwaremaker.com/english/tm1_en.htm). This word processor requires much less memory than OpenOffice.org Writer, but still contains many powerful features. With TextMaker, interchanging documents between different operating systems is easy because there are also versions of TextMaker for Windows, Pocket PCs, Handheld PCs, FreeBSD, and Zaurus.

## Using Traditional Linux Publishing Tools

The first document and graphics tools for Linux were mostly built on older, text-based tools. Despite their age, many of the older publishing tools such as *Graf* and *LaTeX* are still used by people in the technical community. With these old-school text processors, you can ignore document appearance while writing. Plainext macros instruct post-processors how to lay out a document for printing after writing is done. With word processors (such as OpenOffice.org Writer and StarOffice Writer), you mark up text and see the basic layout of the document as you write.

Some attributes of the traditional Linux publishing tools make them particularly well suited for certain types of document publishing. *Graf* and *LaTeX* (which is based on TeX) come with CentOS and have been popular among technical people. Reasons for that include:

- You can manipulate files in plainext. Using tools such as `sed` and `grep`, you can scan and change one document or hundreds with a single command or script.
- Scientific notation is supported. With eqn, you can create complex equations. LaTeX and TeX are suited for technical notation. Some math publications require LaTeX.
- Editing can be faster because traditional Linux documents are created with a text editor. You usually get better performance out of a text editor than a word processor.

Simple page layouts work well with Linux documentation tools. For example, a technical book with a few flow charts and images can be easily produced and maintained using Groff or TeX documentation tools. Letters and memos are also easy to do with these tools. And, of course, Linux man pages are created with text-based tools.

Also, Linux likes PostScript. Most Linux document-processing software includes print drivers for PostScript. There are many tools for converting PostScript to other formats. Some documents on the Web are distributed in PostScript (.ps).

The drawback to the traditional Linux documentation tools is that they are not intuitive. Rarely will a beginner try to use these tools, unless they have a need to support legacy UNIX or Linux documents (such as manual pages or old UNIX guides). Although there are some easier front-ends to LaTeX (see the description of LyX later on, if you are creating documents in a text editor, you need to learn what macros to type into your documents and which formatting and print commands to use.

> **NOTE** For many years, the UNIX system documentation distributed by AT&T was created in troff/nroff formats, which predate Groff. The documents used separate macro packages for man pages and guide material. Using a source code control system (SCCS), thousands of pages of documentation could be ported to different UNIX systems. Today, CentOS includes the same tools to work with man pages.

### Creating Documents in Groff or LaTeX

You can create documents for either of Linux’s Groff (troff/nroff) or LaTeX (TeX) styles of publishing using any text editor. CentOS comes with several text editors, or you can download others from the Internet. See the section “Using Text Editors and Notepads,” earlier in this chapter, for more information.

The process of creating documents in Groff or LaTeX consists of the following general steps:

1. Create a document with any text editor. The document will contain text and markup.
2. Format the document using a formatting command that matches the style of the document that you created (e.g., with groff or latex). During this step, you may need to indicate that the document contains special content, such as equations (eqn command), tables (tb) command), or line drawings (pic command).
3. Send the document to an output device. The device may be a printer or display program.

If you are used to a word processor with a GUI, you may find these publishing tools difficult. In general, Groff is useful to create man pages for Linux. LaTeX is useful if you need to produce mathematical documents, perhaps for publication in a technical journal.
