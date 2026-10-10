You can work with a variety of document, spreadsheet, and image types; not many commerical document types are supported yet. So you may need to import documents using other tools before you can read them into KWord. The KSpread program can open several different spreadsheet styles, however, such as Microsoft Excel and GNumeric spreadsheets. Kivio is a useful flowcharting tool.

# ## Using Traditional Linux Publishing Tools

With old-school text processors (such as Groff and TeX), you can ignore document appearance while writing. Plain-text macros instruct post-processors how to lay out a document for printing after writing is done. With word processors (such as OpenOffice.org Word and StarOffice Writer), you mark up text and see the basic layout of the document as you write.

Some attributes of the traditional Linux publishing tools make them particularly well suited for certain types of document publishing. Groff and LaTeX (which is based on TeX) come with Fedora and RHEL and have been popular among technical people. Reasons for that include:

+   - You can manipulate files in plain text. Using tools such as `sed` and `grep`, you can scan and change one document or hundreds with a single command or script.
+   - Scientific notation is supported. With `gegn`, you can create complex equations. LaTeX and TeX are suited for technical notation. Some math publications require LaTeX.
+   - Editing can be faster because traditional Linux documents are created with a text editor. You usually get better performance out of a text editor than a word processor.

Simple page layouts work well with Linux documentation tools. For example, a technical book with a few flow charts and images can be easily produced and maintained using Groff or TeX documentation tools. Letters and memos are also easy to do with these tools. And, of course, Linux man pages are created with text-based tools.

Also, Linux likes PostScript. Most Linux document-processing software includes print drivers for PostScript. There are many tools for converting PostScript to other formats. Also, some documents on the Web are distributed in PostScript (`.ps`).

The drawback to the traditional Linux document tools is that they are not intuitive. Rarely will a beginner try to use these tools, unless they have a need to support legacy UNIX or Linux documents (such as manual pages or old UNIX guides). Although there are some easier front ends to LaTeX (see the description of LyX later on), if you are creating documents in a text editor, you need to learn what macros to type into your documents and which formatting and print commands to use.