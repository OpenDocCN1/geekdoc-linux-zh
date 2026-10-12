
Icons for launching Writer, Impress, and Calc are placed on the Fedora desktop panel. Alternatively, to open those and other OpenOffice.org applications, click Office from the main menu. Then select the OpenOffice.org application you want to open. Figure 6-1 shows an example of OpenOffice.org Writer displaying and working with a document file that was originally created in Microsoft Word.

![](img/b22364e57409c2481ba806e4e6b9309c_244_0.png)

**Figure 6-1**: Work with Microsoft Word documents in OpenOffice.org Writer.

The controls in OpenOffice.org are similar to the ones you would find in Word. Toolbars include boxes for identifying filenames, changing styles, font types, and font sizes. Buttons let you save and print the file, change the text alignment, and cut, copy, and paste text. In other words, Writer includes almost everything you expect in an advanced word processor. In addition, Writer includes a handy PDF button to output a file directly to the PDF format. This is very useful for exchanging documents or placing data on the Internet.

> **NOTE**: Find out more about OpenOffice.org at www.OpenOffice.org. Also note that technically, the name of the suite is OpenOffice.org, for copyright reasons associated with simply calling it OpenOffice.

Other free word processors that come with Fedora include AbiWord and KOffice (which is part of the KDE desktop). As for commercial offerings, there is StarOffice from Sun Microsystems.

- **StarOffice** — The StarOffice productivity suite contains applications for word processing, spreadsheets, presentation graphics, e-mail, news, charting, and graphics. It was created to run on Linux systems, but it runs in other environments as well. It can import and export a variety of Microsoft file formats. StarOffice is owned by Sun Microsystems, which sells it as a commercial product.

> NOTE: One reason for paying for StarOffice when you can get OpenOffice.org software for free is that you get a bunch of extras with StarOffice. The extras that come with StarOffice include a spellchecker, clip art, many more file converters (although the best ones are for converting Microsoft formats), a database module, and technical support.

- **AbiWord** — The AbiWord word processor (*abiword* command) is produced by the AbiSource project (www.abisource.com). Besides working with files in its own AbiWord format (.abw and .zabw), AbiWord can import files in Microsoft Word and several other formats. If AbiWord is not installed, you can install the abiword package from the DVD that comes with this book.

- **KOffice** — The KOffice package contains a set of office productivity applications designed for the KDE desktop. It includes a word processor (KWord), spreadsheet (KSpread), a presentation creator (KPresenter), and a diagram drawing program (KChart). These applications can be run separately or within a KOffice Workspace. (The KOffice package is on the DVD that comes with this book.)

The StarOffice suite from Sun Microsystems Inc. is a product that runs on Linux, UNIX, and Windows operating systems. Like OpenOffice.org, StarOffice contains many features that make it compatible with Microsoft Office applications. In particular, it includes the capability to import Microsoft Word and Excel files.

StarOffice is probably the most complete integrated office suite for Linux. If you are working in a cross-platform environment, however, you can also get StarOffice for Sun Solaris and Microsoft Windows operating systems. StarOffice includes:

- **StarOffice Writer** — This is the StarOffice word processing application. It can import documents from a variety of formats, with special emphasis on Word documents.
- **StarOffice Calc** — This is the spreadsheet program that comes with StarOffice. You can import spreadsheets from Microsoft Excel and other popular programs.
- **StarOffice Impress** — This module enables you to create presentations.
- **StarOffice Draw** — This is a vector-oriented drawing program. It includes the capability to create 3D objects and to use texturing.
- **StarOffice Base** — You can manage your data with StarBase, a friendly front end for databases. It can access a variety of database interfaces.

There are also other tools in StarOffice that enable you to create business graphics, edit raster images, and edit mathematical formulas (StarOffice Math).

You can download StarOffice 7 for Linux or purchase a boxed set from the StarOffice Web site at www.sun.com/software/star/staroffice/. Although StarOffice was once available free for download, the current price to download the software for home users is $79.95.

> **NOTE**: OpenOffice.org is an open-source project sponsored by Sun Microsystems. Sun takes the OpenOffice.org source code and uses it (along with other modules) to create StarOffice. This is very similar to Mozilla, an open-source Web browser, and Netscape, a commercial product built from the Mozilla sources. Of course, the Fedora Project and Red Hat Enterprise Linux have a similar symbiotic relationship.

## AbiWord

The AbiWord word processor is a very nice, free word processor from the AbiSource project (www.abisource.com). If you are creating documents from scratch, AbiWord includes many of the basic functions you need to create good-quality documents.

With AbiWord, you can select what type of document the file contains. You can select to read the file in the following formats:

- AbiWord (.abw)
- GZipped AbiWord (.zabw)
- Rich Text Format (.rtf)
- Microsoft Word (.doc)
- UTF8 (.utf8)
- Text (.txt)

AbiWord doesn't yet import all of these file types cleanly. Although the recent version of AbiWord supports Word styles, sometimes tables, graphics, and other features don't translate perfectly. If you want to work with a Word document in AbiWord, open it as AbiWord, correct any font problems, and save the document in AbiWord format. AbiWord has vastly improved in the past few releases, so you can still have problems if you need to exchange files with others who are using Word. (To keep files in the Word format, OpenOffice.org and StarOffice work much better, but not perfectly.)

AbiWord is a great first try as a usable word processor. Recently added features, such as styles and bullets, continue to make AbiWord a more useful word processing tool. It’s not competitive with comparable commercial products, but its developers continue to improve it.

## Using KOffice

There is now a KDE office suite of applications that go with the KDE desktop. The KOffice package has the basic applications you would expect in an integrated office suite: a word processor (KWord), spreadsheet (KSpread), a presentation creator (KPresenter), and a diagram drawing program (KChart).

You can start by opening the KOffice Workspace (from the red hat menu, Office → KOffice Workspace). From the workspace window that opens, you can select from the different office applications from the left column. Open multiple documents in any of the applications. Then click on Documents in the left column to choose which one to display at the moment.

Figure 6-2 shows the KOffice workspace, displaying a KWord document.

![](img/b22364e57409c2481ba806e4e6b9309c_247_0.png)

**Figure 6-2**: The KOffice Workspace lets you work with multiple KDE office applications at once.

You can work with a variety of document, spreadsheet, and image types; not many commercial document types are supported yet. So you may need to import documents using other tools before you can read them into KWord. The KSpread can open several different spreadsheet styles, however, such as Microsoft Excel and GNumeric spreadsheets. Kivio is a useful flowcharting tool.

With old-school text processors (such as Groff and TeX), you can ignore document appearance while writing. Plain-text macros instruct text-processors how to lay out a document for printing after writing is done. With word processors (such as OpenOffice.org Word and StarOffice Writer), you mark up text and see the basic layout of the document as you write.

Some attributes of the traditional Linux publishing tools make them particularly well suited for certain types of document publishing. Groff and LaTeX (which is based on TeX) come with Fedora and have been popular among technical people. Reasons for that include:

- You can manipulate files in plain text. Using tools such as sed and grep, you can scan and change one document or hundreds with a single command or script.
- Scientific notation is supported. With \( egexp \), you can create complex equations. LaTeX and TeX are suited for technical notation. Some math publications require LaTeX.
- Editing can be faster because traditional Linux documents are created with a text editor. You usually get better performance out of a text editor than a word processor.

Simple page layouts work well with Linux documentation tools. For example, a technical book with a few flow charts and images can be easily produced and maintained using Groff or TeX documentation tools. Letters and memos are also easy to do with these tools. And, of course, Linux man pages are created with text-based tools.

Also, Linux likes PostScript. Although people think of PostScript as a printing language, it is really more of a programming language (you can write PostScript code directly). Most Linux document-processing software includes print drivers for PostScript. Also, some documents on the Web are distributed in PostScript (.ps).

The drawback to the traditional Linux document tools is that they are not intuitive. Although there are some easier front-ends to LaTeX (see the description of LyX later on), if you are creating documents in a text editor, you need to learn what macros to type into your documents and which formatting and print commands to use.

> **NOTE**: For many years, the UNIX system documentation distributed by AT&T was created in troff/nroff formats, which predate Groff. The documents used separate macro packages for man pages and guide material. Using a source code control system (SCCS), thousands of pages of documentation could be ported to different UNIX systems. Today, Fedora still includes the same tools to work with man pages.

You can create documents for either of Linux’s Groff (troff/nroff) or LaTeX (TeX) styles of publishing using any text editor. Fedora comes with several text editors, or you can download others from the Internet. See the “Choosing a Text Editor” sidebar for more information.
