
```xml
<xml version="1.0">
<article>
  <title>Choosing a new car</title>
  <artheader>
    <abstract>
      In this article, you will learn how to price,
      negotiate for, and purchase an automobile.
    </abstract>
  </artheader>
  <section>
    <title>Getting Started</title>
    <para>
      The first thing you will learn is how to figure out
      what you can afford.
    </para>
  </section>
  <section>
    <title>The Next Step</title>
    <para>
      After you know what you can afford, you can begin your
      search.
    </para>
  </section>
</article>
```

You notice a few things about this document. The entire document is wrapped in article tags (<article> </article>). The article title is in title tags (<title></title> The section tags (<section> </section>) indicate sections of text that have a title and paragraph. These sections can later be treated separately in the TOC.

- 4. Save the file and exit from the text editor.
- 5. Next, you can try translating the document you created into several different formats. For example, to create HTML output you can get the following:

$ db2html cardoc.sgml

The result is a new directory called cardoc. The result from db2html in the cardoc directory was: stylesheets-image, t2.html, and x12.html.

- 6. To view the HTML file you just created, I followed the following:

$ firefox $HOME/doctype/cardoc/t2.html

6-6 shows an example of the output created from the db2html command. The screen on the left shows the first page. Click the Next link at the top of the page. The second page that you see is on the right. During conversion to HTML, the db2html command adds Next/Previous buttons to each page. It also puts the title of each section in a Table of Contents on page one and in a browser's title bar.

From this point, you can continue to add content and different types of tags. If you are writing documents for a particular project (such as the Linux projects mentioned earlier), you should get information on the particular tags and other style issues they require.

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_313_0.png)

Figure 6-6: The DocBook file is output in HTML with the db2html command.

# Converting DocBook documents

The previous example shows how to create a DocBook document and convert it to HTML output. The following and RHEL utilities convert DocBook to other formats:

- docbook2dvi - Converts a DocBook file to Device Independent format.
- docbook2html - Converts a DocBook file to HTML format.
- docbook2man - Converts a DocBook file to man page.
- docbook2pdf - Converts a DocBook file to Portable Document Format (PDF).
- docbook2rtf - Converts a DocBook file to Rich Text Format (RTF).
- docbook2tex - Converts a DocBook file to TeX format.
- docbook2xi - Converts a DocBook file to GNU TeXInfo format.
- docbook2txt - Converts a DocBook file to a bare text format.

# Displaying PDF Files with Adobe Acrobat Reader

Non-WYSIWYG publishing can be very paper-intensive if you send a Groff or LaTeX document to the printer each time you want to make a change to the document’s content or formatting. To save paper and time spent around, you can use some print preview programs to display a document on a screen as it will appear on the printed page. The following sections describe the Adobe Reader for displaying Portable Document Format (PDF) files.

The Portable Document Format (PDF) provides a way of storing documents as they would appear in print. With Adobe Acrobat Reader, you can view PDF files in a very friendly way. Adobe Acrobat makes it easy to move around a PDF file. A PDF file may include hyperlinks, a table of contents, graphs, and a variety of type fonts.

A recent version of the Adobe Acrobat Reader (version 8) is available in RPM format from Adobe.com. This version can use many PDF features that aren't available in other PDF readers, including some new compression features in version 1.4. (While you are writing documents for a particular project (such as the Linux projects mentioned earlier), you should get information on the particular tags and other style issues they require.)

# Chapter 6: Publishing with Fedora and RHEL 267
