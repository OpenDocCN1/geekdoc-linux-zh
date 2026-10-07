
# Software Developers

DocBook is ideal for software developers who are working on documentation as they write software. Because DocBook does not require a word processor, developers who work in a text editor such as vi or Emacs can work on documentation simultaneously.

DocBook also provides markup elements specifically suited for documenting about any type of software. Chapter 7, "Collaborative Work," walks you through using DocBook on collaborative projects, including how to use DocBook with CVS. If Vim is your favorite text editor, Chapter 8, "Using Vim," shows how you can Vim syntax highlighting and other features making editing DocBook files. If Emacs is your editor of choice, Chapter 9, "Using Emacs" walks you through all the advanced Emacs features designed to simplify editing DocBook documents.

# Who Should Not Read This Book

Okay, DocBook is not for everyone. It's true—some writing tasks don't require the power and flexibility of DocBook. You probably don't need DocBook to write a letter or make up a grocery list. If you don't do a lot of writing, you probably won't have to use a markup language to handle your formatting. Although we don't think DocBook is particularly complicated, using DocBook to write a letter or do very simple documents is like using a shotgun to kill flies.

Make no mistake—learning DocBook will require an investment of time and effort. If you don't have to produce professional or academic-quality documents, you probably don't need DocBook.

# Conventions

The following is a list of conventions that you will find in DocBook Publishing. On the CD-ROM you will find the DocBook template to create this book, and you will also find sample code that you can compare with the book to see how we marked up the chapters.

> Cautions generally tell you how to avoid problems.

![](img/81f56bf497dbf7f7582072400d12cb42_20_0.png)

# Introduction

DocBook markup, or other code, looks like this in the book:

```
<!DOCTYPE docbook PUBLIC "//OASIS//DTD DocBook V3.1//EN [
  <!ENTITY introduction SYSTEM "introduction.sgm">
  <!ENTITY chap SYSTEM "chap.sgm">
>
```

![](img/81f56bf497dbf7f7582072400d12cb42_21_0.png)

Buzzwords are terms that aren't used in everyday speech but are useful to know when dealing with DocBook.

```
<bookinfo>
  <date>2000-07-11</date>
  <title>DocBook Publishing</title>
  <subtitle><trademark class="registered">A Gentle Guide to DocBook</subtitle>
</bookinfo>
&introduction;
&chap;
</book>
```

![](img/81f56bf497dbf7f7582072400d12cb42_21_1.png)

> Notes provide additional helpful or interesting information.

![](img/81f56bf497dbf7f7582072400d12cb42_21_2.png)

> Tips often suggest techniques and shortcuts to make your life easier.

# What's Included

DocBook Publishing should be a complete resource, we've included some extra goodies. Also, to get additional information and news about DocBook, be sure to visit the Web site that accompanies this book (http://www.ZonkerBooks.com).

The CD-ROM includes all the necessary software and DTDs to use DocBook, so you don't have to hunt all over the Internet. Everything on the CD-ROM is current at the time of this writing, but it may be outdated by the time you read this book. You don't necessarily have to have the latest versions to produce documentation with DocBook, you might want to stay current. Luckily, DocBook does not change frequently, or radically, so this text should remain current for quite some time.

In addition to the DTDs, Jade, and SGMLTools-lite, we have included templates for many types of documents on the CD-ROM. All the examples used in DocBook Publishing are included on the CD-ROM, as well as templates for MLA-style academic papers, indexes, books, articles, and Web-based manuals. No matter what you use DocBook, for one of the bare-bones templates included on the CD-ROM we give you a jump-start.

# What Is DocBook?

So, what is this DocBook stuff anyway? Technically, DocBook is an SGML or XML Document Type Definition—DTD, for short (more on SGML and XML in a moment). However, DocBook is often used to refer to the parsing tools, sheets, and other tools used to work with DocBook collectively. Generally speaking, when the term DocBook is used in this work, it refers to the entire collection of tools used to produce documentation in DocBook, not just the DTD and sheets.

# History of DocBook

Obviously, DocBook did not magically appear. In one form or another, it has been around since 1991. DocBook began life as a DTD designed by O'Reilly and Associates and Hal. Computer Systems to help convert UNIX documentation into an easily readable format.

O'Reilly then passed DocBook to the Davenport Group, an organization created by O'Reilly and Associates to provide a forum for companies and organizations.

# OASIS

OASIS is a nonprofit international consortium. It creates standards for open innovation. OASIS was formed in 1999 to promote the development of open standards for the e-commerce and related technologies. OASIS is also known for its work on XML and SOAP.

# DocBook and Open Source

DocBook is an open standard, which means that anyone can use, modify, and distribute it. This has allowed a large community of developers to contribute to the project. There are many open-source tools that use DocBook, including editors and processors.

# Buzzword

Metanguage is a definition or description of language. Meta is a prefix that, depending on context, refers either to change (as in metamorphosis) or, to information, something more comprehensive (as in metadata).

# SGML/XML

SGML is a metanguage used to define rules for how a document can be described. SGML DTDs spell out what markup is allowed and how to use. For example, HTML is an SGML DTD. In HTML, the DTD is the full description of the HTML language, and it offers information about HTML markup. If you've ever used XML, you know that the DTD tells a browser `<b>` makes text bold, `<i>` makes text italic, and `<img>` describes the attributes of an image—including where the image can be found and possibly the height, width, and alignment for the text. However, because the DTD does not describe a `<wohoo>` tag, browsers will probably ignore it or render it poorly.

XML, as mentioned before, is a subset of SGML. XML is an official recommendation from the W3C—the World Web Consortium, the organization responsible for HTML specifications. XML is actually a set of specifications for documentation that are designed to be SGML-compatible, human and machine readable, and Web friendly, making the creation of documents easy. That's a tall order, but the W3C has been successful in creating a recommendation that is being adopted even before the final specification is approved.

XML is used for a number of tasks. Microsoft is using XML to some extent in its Office file formats, many programs use XML configuration files, and a few companies use XML to exchange data with one another for business-to-business transactions over the Internet. That's just a few of XMLs other roles, aside the XML DocBook DTD.

![](img/81f56bf497dbf7f7582072400d12cb42_23_0.png)
