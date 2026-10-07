
## Chapter 5: Making Online Documents

```html
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 4.01//">
<html
<Head>
  <meta name="generator" content="HTML Tidy. see www.w3.org">
  <title>Sample HTML Document</title>
  <meta name="GENERATOR" content="
  Modular DocBook Stylesheet Version 1.57">
</Head>
<body class="CHAPTER">
  <div class="CHAPTER">
    <h1><a name="CH1">Chapter 1. Sample Document</a></h1>
  </div>
  <div class="SECTION1">
    <h1 class="SECTION1"><a name="W1">Introduction</a></h1>
    <p>This is a Docbook converted to HTML. Not too flashy, but it works!</p>
  </div>
</body>
</html>
```

"1.html" 22L, 50OC

![](img/81f56bf497dbf7f7582072400d12cb42_137_0.png)

If you want to clean up the file more and add some tabbed indenting, you can use the following command:

```
tidy -m index.html -i -clean
```

This takes the index.html file, indents it to make it easily readable, and modifies it in place—in other words, the file is written out to index.html. I also prefer to throw the -o option in there, which strips optional end tags such as the paragraph end. Figure 5.12 shows output from HTML Tidy, indented to make the code easier to read.

HTML Tidy is not required, but it certainly makes your HTML output much cleaner.

## Integrating Images

Chapter 3, "Using Images," covers in great depth how to include images in your document, so I won’t revisit old territory. However, it bears repeating that the only image types consistent with outputting HTML are GIF, JPEG, and PNG images. If you are anticipating an audience that is using the latest browser, I recommend PNGs. However, if you're expecting an audience that is still using older browsers (3.x or lower), you might want to stick with JPEGs. Be sure to check out Chapter 6 for the whole story.

## Testing Output

Testing your output is easy. Fire up your favorite Web browser, and open up the files produced by SGMLTools. However, I can't stress the importance of testing your output thoroughly. No matter how careful you've been, there's a good chance that a broken link exists somewhere in your document, and you don't want to annoy your audience with broken links.

You should also make sure that you can view your document in Lynx and the images are represented by Alt tags so that any audience that is using Lynx or vision-impaired can enjoy the document as well.

Test all links at least once from the Web browser of your choice. If you're picky, you can test them in multiple browsers to see how they appear.

## Summary

This chapter covers the aspects of writing DocBook for output to HTML. In particular, the chapter focuses on linking between various parts of the document and resources located on the Web.

Even if you don't plan to output to HTML for online now, I very much encourage you to write your documents as if you are going to. Although it might take longer, it will save you a great deal of time later. If you try to go back and “webalize” your documents after the fact, you won't remember everything you wrote (not as well), and the links to resources in the document will be lost.

It doesn't hurt a document being output to PostScript to have the extra elements necessary for HTML output, but it is a big pain to convert the document later.

## Chapter 6: Parsing DocBook

### Getting the Current DTD

Installing the DTDs and Stylesheets

- Jade — James' DSSSL Engine

- OpenJade

- Using SGMLtools-Lite and SGMLtools

- Using Other Tools with DocBook

now you've gone through a few chapters, and you have actual DocBook documents from which you want to produce output.

If you haven't created any documents yet, you might want to go back through the first several chapters and create one. If you are just going to be parsing documents sent to you by other authors, feel free to grab one of the DocBook templates off the CD-ROM included with this book.

![](img/81f56bf497dbf7f7582072400d12cb42_141_0.png)

In this chapter you will look at how to configure a Linux or UNIX-type system and produce output from your documents. We will also touch on some Windows-based solutions, but the main processing tool in this chapter, SGMLtools, is not available on Windows.

Before you can process DocBook and render it into new formats, you must acquire the DTD, stylesheets, and assorted modules if they're not already installed on your system.

### Getting the Current DTD

The first step is to get the DocBook DTD and the stylesheets. The best place to get these is from the official DocBook site at http://www.oasis-open.org/docbook/. You can find both current SGML and XML DTDs as well as older versions archived on the site for historical reasons. You can download all the necessary files individually, or in a archive.

### SGML

The SGML DTD is found at http://www.oasis-open.org/docbook/sgml/index.html (see Figure 6.1). If you're curious about what older (and simpler) versions of the DocBook looked like, download the DocBook DTD version 1.0. While I don't recommend using the 1.0 DTD, it's very educational to open it and look at what's going on in a DTD. It's certainly much easier to browse through the current collection of files that make up DocBook. You will notice that the original DocBook DTD was only one file of about 683 lines. The latest version, 4.1, is 14 files that add up to approximately 10,630 lines! DocBook has certainly grown since 1992. Aren't you glad you didn't have to write your own DTD?

### XML

The Official DocBook site also has all the necessary files for using DocBook XML. At the time of writing, the OASIS DocBook site is being reconstructed from some sort of crash. I've tested all the URLs in the book, and they are all working at the time of writing. However, some links on the site are still broken. It is hoped that they will be fixed soon, but if not, you can check the other DocBook site, at http://www.docbook.org.

In addition to the XML DTD and stylesheets, there are also DTDs and examples on the site for EBNF, HTML forms, and MathML.

> EBNF is an extension to the XML DocBook DTD used to create diagrams in the extended Backus-Naur form (EBNF). It is new to versions 4.1.2 and later of the XML DTD.

If you do not require EBNF, HTML forms, or MathML, you may not need those files unless you receive documents with that sort of markup in them.

When you use the DocBook XML DTD, you must also have the XML ISO Entity sets, which are distributed separately on the DocBook site at http://www.docbook.org/xml/4.1.2/ent/ (see Figure 6.2). The DocBook Technical Committee does not create or maintain the ISO Entity sets but provides them out of necessity.

![](img/81f56bf497dbf7f7582072400d12cb42_143_0.png)

Figure 6.2 The DocBook XML DTD page

### Installing the DTDs and Stylesheets

If, for some reason, you already have a set of DTDs, but you're not sure whether you have the XML or SGML DTDs, check the filenames. Most DocBook XML filenames have xml in them to identify them as XML. For instance, the main DocBook SGML DTD filename is docbook.dtd; the XML DTD is named docbook.xml.

Note that none of the DocBook files indicate which version number of DocBook they are. If you have more than one version of the DTDs floating around, be sure to put them in separate folders.

### Installing the DTDs and Stylesheets

When you have the files containing the DocBook DTD and stylesheets, you put them into their own directory. If you downloaded them from the DocBook site, copy the ZIP file into a directory. Unzip it with WinZip if you're on Windows or with unzip if you're on Linux or a UNIX-type operating system.

It doesn't matter where you put the DocBook directory and files. Some popular locations on UNIX-type operating systems are under the /usr/local

> Because the world is a fast-moving place, I'm including notes on how to install the DocBook DTD here. It's quite likely that the time this book is written and the time it is published, a new version of the DocBook DTDs will become available. However, to make life simple, I've included the DocBook DTDs in three package formats for easy installation on Linux systems. You can find packages on the CD-ROM in tgz format, the Red Hat Package Manager format, and the Debian package format. One of these should work on your system. I'll also try to keep updated install packages on my site, at http://www.ZonkerBooks.net/.

Hopefully, you won't need these instructions. However, it's good to have them. Check the README files in the directories for installation instructions for the Linux packages.

![](img/81f56bf497dbf7f7582072400d12cb42_144_0.png)

For Windows users, you might want to place them under C:\docbook\sgml\ or C:\docbook\xml\, depending on which version you're using.
