
When you create a Web page with tkWWW in editor mode, you can then flip modes to browser to see the same page properly formatted. In editor mode, most of the formatting is correct, but the tags are left visible. This makes for fast development of a Web page. Unfortunately, tkWWW must rely on Tk for its windowing, which tends to slow things down a bit on average processors. Also, the browser aspect of tkWWW is not impressive, using standard Tk frames. However, as a prototyping tool, tkWWW is very attractive, especially if you know the Tcl language.

Another option is to use an HTML filter. HTML filters are tools that let you take a document produced with any kind of editor (including ASCII text editors) and convert the document to HTML. Filters are useful when you work in an editor that has a proprietary format, such as Word.

HTML filters are attractive if you want to continue working in your favorite editor and simply want a utility to convert your document with tags to HTML. Filters tend to be fast and easy to work with, because they take a filename as input and generate an HTML output file. The degree of error checking and reporting varies with the tool.

There are filters available for most types of documents, many of which are available directly for Linux, or as source code that can be recompiled without modification under Linux. Word for Windows and Word for DOS documents can be converted to HTML with the CU_HTML and ANT_HTML extensions mentioned earlier. A few stand-alone conversion utilities have also begun to appear. The utility WP2OHTML converts Word Perfect documents to HTML. WP2OHTML is a set of macros for Word Perfect versions 5.1 and 6.0. The Word Perfect filter can also be used with other word processor formats that Word Perfect can import.

FrameMaker and FrameBuilder documents can be converted to HTML format with the tool FM2HTML. FM2HTML is a set of scripts for converting Frame documents to HTML, while preserving hypertext links and tables. It also handles GIF files without a problem. Because Frame documents are platform independent, Frame documents developed on a PC or Macintosh could be moved to the Linux platform and FM2HTML executed there.

### Note

A copy of FM2HTML is available by anonymous FTP from bang.nta.no in the directory /pub. The UNIX set is called fm2html.tar.v.0.n.m.Z

![](img/e8e6b47ac20475e23d48b4c476f5d891_900_0.png)

LaTeX and TeX files can be converted to HTML with several different utilities. There are quite a few Linux-based utilities available, including LATEXTOHTML, which can even handle inline LaTeX equations and links. For simpler documents, the utility VULCANIZE is faster but can’t handle mathematical equations. Both LATEXTOHTML and VULCANIZE are Perl scripts.

> **Note**
LATEXTOHTML is available through anonymous FTP from ftp.tex.ac.uk in the directory pub/archive/support as the file latextohml. VULCANIZE can be obtained from the Web site http://www.cis.upenn.edu/~mjd/vulcanize.html.

RTFTOHTML is a common utility for converting RTF format documents to HTML. Many word processors handle RTF formats, so an RTF document can be saved from your favorite word processor and then RTFTOHTML run to convert the files.

> **Note**
RTFTOHTML is available through http://www.w3.org/hypertext/www/tools/rtftohml-2.6.html.

### Maintaining HTML

Once you have written a Web document and it is available to the world, your job doesn’t end. Unless your document is a simple text file, you will have links to other documents or Web servers embedded. These links must be verified at regular intervals. Also, the integrity of your Web pages should be checked at intervals, to ensure that the flow of the document from your home page is correct.

There are several utilities available to help you check links and also to scan the Web for other sites or documents you may want to provide a hyperlink to. These utilities tend to go by a number of names, such as robot, spider, or wanderer. They are all programs that move across the Web automatically, creating a list of Web links that you can access. (Spiders are similar to the Archie and Veronica tools for the Internet, although neither of these cover the Web.)

Although they are often thought of as utilities for users only (to get a list of sites to try), spiders and their kin are useful for document authors, too, because they show potentially useful and interesting links. One of the best known spiders is the World Wide Web Worm, or WWW. WWW enables you to search for keywords or create a Boolean search and can cover titles, documents, and several other search types (including a search of all known HTML pages).

A similarly useful spider is WebCrawler, which is similar to WWW except it can scan entire documents for matches of any keywords. It displays the result in an ordered list from closest match to least likely match.

### Note

> A copy of World Wide Web Worm can be obtained from http://www.cs.colorado.edu/home/mcbryan/WWW.html. WebCrawler is available from http://www.biotech.washington.edu/WebCrawler/WebCrawler.html.

A common problem with HTML documents as they age is that links that point to files or servers may no longer exist (because either the locations or the documents have changed). It is therefore good practice to validate the hyperlinks in a document on a regular basis. A popular hyperlink analyzer is HTML_ANALYZER. It examines each hyperlink and the contents of the hyperlink to ensure that they are consistent. HTML_ANALYZER functions by examining a document for all links, and then creating a text file that has a list of the links in it. HTML_ANALYZER uses the text files to compare the actual link content to what it should be.

HTML_ANALYZER actually does three tests: It validates the availability of the documents pointed to by hyperlinks (called validation); it looks for hyperlink contents that occur in the database but are not themselves hyperlinks (called completeness); and it looks for a one-to-one relation between hyperlinks and the contents of the hyperlink (called consistency). Any deviations are listed for the user.

HTML_ANALYZER users should have a good familiarity with HTML, their operating system, and the use of command-line driven analyzers. The tool must be compiled using the make utility prior to execution. There are several directories that must be created prior to running HTML_ANALYZER, and when it runs, it creates several temporary files that are not cleaned up. Therefore, HTML_ANALYZER is not a good utility for a novice.

## HTML Programming Basics

HyperText Markup Language (HTML) is quite an easy language to learn and work with, and as new versions have been introduced over the last few years it has become quite powerful, too. We can’t hope to teach you HTML in a single chapter in this book, but we can give you an overview of the language and how to use the basics to produce a simple Web page or two.

If you’ve seen a Web page before, you have seen the results of HTML. HTML is the language used to describe how the Web page will look when you access the site. The server transfers the HTML instructions to your browser, which converts those HTML lines of code into the text, images, and layouts you see on the page. A Web browser is usually used to access HTML code, but there are other tools that can do the same. There are a wide variety of browsers out there, starting with the granddaddy of them all, NCSA’s Mosaic. Netscape’s Navigator is the most widely used browser right now, although Microsoft is making inroads slowly with its Explorer. The browser you use doesn’t matter, as they mostly do the same job—display the HTML code they receive from the server. A browser is almost always acting as a client, requesting information from the server.

The HTML language is based on another language called SGML (Standard Generalized Markup Language), which is used to describe the structure of a document and allow for better migration from one documenting tool to another. HTML does not describe how a page will look; it’s not a page description language like PostScript. Instead, HTML describes the structure of a document. It will indicate which text is a heading, which is the body of the document, and where pictures should go. However, it does not give explicit instructions on how the page will look; that’s up to the browser.

Why use HTML? Primarily because it is a small language, and so can transfer instructions over a network quickly. HTML does have limitations because of its size, but newer versions of the language are expanding the capabilities a little. The other major advantage of HTML is one most people don’t think about: It is device independent. It doesn’t matter what machine you run; a Web browser will take the same HTML code and translate it for the platform. The browser is the part that is device dependent. That means you can use HTML to write a Web page and not care what machine is used to read it.

## What Does HTML Look Like?

HTML code is pretty straightforward, as you will see. For the most part it consists of a bunch of “tags” which describe the beginning and ending of a structure element (such as a heading, paragraph, picture, table, and so on). For each element, there should be a
