
## AbiWord
perfectly. If you want to work with a Word document in AbiWord, open it as AbiWord, correct any font problems, and save the document in AbiWord format. AbiWord has vastly improved in the past few releases, but you can still have problems if you need to exchange files with others who are using Word. (To keep files in the Word format, OpenOffice.org and StarOffice work much better, but not perfectly.)

If you have slow hardware, AbiWord offers better performance than OpenOffice.org Writer. If you are working in a cross-platform environment, you can get versions of AbiWord that run in Windows, Mac OS X, QNX, and most UNIX derivatives (Linux, BSD, Solaris, and so on).

Recently added features, such as styles and bullets, continue to make AbiWord a more useful word processing tool. It’s not competitive with comparable commercial products, but its developers continue to improve it.

### Using KOffice

There is a KDE office suite of applications that go with the KDE desktop. The KOffice package has the basic applications you would expect in an integrated office suite: a word processor (KWord), spreadsheet (KSpread), a presentation creator (KPresenter), and a diagram drawing program (KChart).

Use the command `yum install koffice-suite` to install the KOffice suite. When you use KOffice, you can select from the different office applications from the left column. Open multiple documents in any of the applications. Then click Documents in the left column to choose which one to display at the moment.

Figure 6-2 shows KWord displaying a Word document.

![](img/fb202c163797a743c3c6cf236316bc96_290_0.png)

Figure 6-2: You can work with Word documents in KWord.

You can work with a variety of document, spreadsheet, and image types; not many commercial document types are supported yet. So you may need to import documents using other tools before you can read them into KWord. The KSpread program can open several different spreadsheet styles, however, such as Microsoft Excel and GNumeric spreadsheets. Kivio is a useful flowcharting tool.

## Using Traditional Linux Publishing Tools

With old-school text processors (such as Groff and TeX), you can ignore document appearance while writing. Plain-text macros instruct post-processors how to lay out a document for printing after writing is done. With word processors (such as OpenOffice.org Word and StarOffice Writer), you mark up text and see the basic layout of the document as you write.

Some attributes of the traditional Linux publishing tools make them particularly well suited for certain types of document publishing. Groff and LaTeX (which is based on TeX) come with Fedora and RHEL and have been popular among technical people. Reasons for that include:

- You can manipulate files in plain text. Using tools such as `sed` and `grep`, you can scan and change one document or hundreds with a single command or script.
- Scientific notation is supported. With `gegn`, you can create complex equations. LaTeX and TeX are suited for technical notation. Some math publications require LaTeX.
- Editing can be faster because traditional Linux documents are created with a text editor. You usually get better performance out of a text editor than a word processor.

Simple page layouts work well with Linux documentation tools. For example, a technical book with a few flow charts and images can be easily produced and maintained using Groff or TeX documentation tools. Letters and memos are also easy to do with these tools. And, of course, Linux man pages are created with text-based tools.

Also, Linux likes PostScript. Most Linux document-processing software includes print drivers for PostScript. There are many tools for converting PostScript to other formats. Also, some documents on the Web are distributed in PostScript (`.ps`).

The drawback to the traditional Linux document tools is that they are not intuitive. Rarely will a beginner try to use these tools, unless they have a need to support legacy UNIX or Linux documents (such as manual pages or old UNIX guides). Although there are some easier front ends to LaTeX (see the description of LyX later on), if you are creating documents in a text editor, you need to learn what macros to type into your documents and which formatting and print commands to use.

> **NOTE:** For many years, the UNIX system documentation distributed by AT&T was created in troff/nroff formats, which predate Groff. The documents used separate macro packages for man pages and guide material. Using a source code control system (SCCS), thousands of pages of documentation could be created to different UNIX systems. Today, Fedora and RHEL include the same tools to work with man pages.

## Creating Documents in Groff or LaTeX

You can create documents for either of Linux’s Groff (troff/nroff) or LaTeX (TeX) styles of publishing using any text editor. Fedora and RHEL come with several text editors, or you can download others from the Internet. See the sidebar “Choosing a Text Editor” for more information.

The process of creating documents in Groff or LaTeX consists of the following general steps:

1. Create a document with any text editor. The document will contain text and markup.
2. Format the document using a formatting command that matches the style of the document that you created (for example, with groff or latex). During this step, you may need to indicate that the document contains special content, such as equations (eqn command), tables (tbl command), or line drawings (pic command).
3. Send the document to an output device. The device may be a printer or display program.

If you are used to a word processor with a GUI, you may find these publishing tools difficult. In general, Groff is useful to create man pages for Linux. LaTeX is useful if you need to produce mathematical documents, perhaps for publication in a technical journal.

## Text processing with Groff

The nroff and troff text formatting commands were the first interfaces available for producing typeset quality documents with the UNIX system. They aren’t editors; rather, they are commands that you send your text through, with the result being formatted pages:

- **nroff** — Produces formatted plain text and includes the ability to do pagination, indents, and text justification, as well as other features.
- **troff** — Produces typeset text, including everything nroff can do, plus the ability to produce different fonts and spacing. The troff command also supports kerning.

The groff command is the front end for producing nroff/troff documentation. Because Linux man pages are formatted and output in Groff, most of the examples here help you create and print man pages with Groff.

People rarely use primitive nroff/troff markup. Instead, there are common macro packages that simplify the creation of nroff/troff-formatted documents:

- **man** — The man macros are used to create Linux man pages. You can format a man page using the -man option to the groff command.
- **mm** — The mm macros (memorandum macros) were created to produce memos, letters, and technical white papers. This macro package includes macros for creating a table of contents, lists of figures, references, and other features that are helpful for producing technical documents. You can format an mm document using the -mm groff option.
- **me** — The me macros were popular for producing memos and technical papers on Berkeley UNIX systems. Format an me document using the -me groff option.

## Choosing a Text Editor

Hardcore UNIX or Linux users tend to edit files with either the vi or emacs text editor. These editors have been around a long time and are hard to learn, but efficient to use. (Your fingers never leave the keyboard.) The emacs editor has some GUI support, although it will run fine in a Terminal window. There are also GUI versions of vi such as GVim (gvim command is in the vim-X11 package), while emacs itself supports menus and mouse features in a GUI.

Some of the other, simpler text editors that can run on your graphical desktop are:

- **gedit** (`gedit` command) — This text editor, which comes with Fedora and RHEL, is the lightweight text editor for GNOME. It has simple edit functions (cut, copy, paste, and select all) and settings let you set indentations and word wrap. Special functions, such as a spell checker and a diff feature are included. You can start `gedit` by typing **gedit** from a Terminal window. Go to `gedit.sourceforge.net` for more information.
- **nedit** (`nedit` command) — While being quite simple to use, nedit offers many nice extras accessible from its menu bar. As you edit, you can run shell commands to sort, count, or spell the contents of your text documents. (You may need to install the `tcshe` package for those features to work.)
- **Advanced Editor** (`kwrite` command) — This text editor includes a menu bar to create, open, or save files. It also has simple edit functions (cut, copy, paste, undo, and help). Other edit features let you set indents, find and replace text, and select all text. This tool comes with the KDE desktop.
- **Text Editor** (`kedit` command) — Another simple text editor. Features let you open files from your file system or from a URL. It also includes a convenient toolbar and a spell checker. It comes with the KDE desktop.
- **joe** (`joe` command) — joe is a text-mode editor that is much simpler than either vi or emacs. joe also has the ability to mimic other text editors, such as vi, emacs, pico, and even the late, lamented WordStar. In addition to standard features such as search and replace, arrow key movements for the cursor, and so on, joe also offers macros, code editing features, and the ability to move or format large chunks of text easily.
