
## What Is DocBook?

For more information on XML, check out Appendix C, “More DocBook Resources, for more XML resources.

## Markup Languages

We've mentioned already that XML, HTML, and SGML are markup languages. What does that mean?

A markup language is a set of elements used to describe how data should be handled. For instance, as mentioned earlier in the chapter, the HTML `<b>` tags tell a browser how to handle text that is enclosed within those tags: Make it bold. DocBook is an SGML DTD that describes the use of all HTML tags. A well-formed HTML document fits completely within the definition of the HTML DTD, and no elements in the document are missed or not present in the HTML DTD.

DocBook is also a markup language. We explained what a markup language is but not necessarily what its benefits are. A markup language enables the author to specify what a piece of text is supposed to be—bold, italic, emphasized, code, a level-one header, and so on—without worrying about how text is formatted. It allows for abstraction, basically, and removes the author from dealing with formatting directly.

## SGML

The SGML DTD for DocBook is the most widely used, and for quite some time the SGML was the only official DTD for DocBook.

Although standards organizations like to emphasize whether something is the official standard, in practice this doesn't amount enough to make much. HTML, for example, has a standard that is approved by the W3C. However, the actual practice is that Microsoft Internet Explorer, Netscape Navigator, and many other browsers support that that are deprecated. They don't support tags that are part of the official standard and also support proprietary tags invented by their research companies in their quest to rule the Web and make their browsers the dominant browser.

The rush to start adopting XML has not been hindered because it is not an official standard (at least).

Although it would be a wonderful world if everyone agreed to follow the standards these organizations put out, that's unlikely to happen anytime.

## Buzzword

Well-formed means that a document does not stray from the standard set by a DTD. The term appears throughout this book; documents that are not formed are likely to be rendered properly. Learning to create well-formed DocBook documents according to either the SGML or XML DTD is the focus of this work. We do not describe any of the shortcuts available in the SGML DocBook DTD because they do not work with each DocBook parser. Therefore, we would lose the portability of DocBook by using them.

![](img/81f56bf497dbf7f7582072400d12cb42_24_0.png)

> NOTE

The version of the SGML DTD used in this book is 4.1. If you get hold of documents written with earlier versions of DocBook, the DocBook.org Web site does archive earlier versions of the DTD—mostly for historical purposes. If you are using a Linux distribution that comes with DocBook DTDs and stylesheets already-installed, check whether they're the latest version. If you are using something from the 3.x series, you will need to upgrade because there are incompatibilities between major versions of the DocBook DTD.

## XML and the Future

If you are brand new to DocBook and SGML, we heartily recommend that you think about using the XML DTD instead of the SGML DTD. It isn't that the XML DTD is better; rather, it seems that more organizations are standardizing XML technologies. Theoretically, other than minor differences, the XML and SGML versions are the same, so it is also possible to learn both, if necessary, without too many headaches.

The XML DTD version described in this book is 4.1.2. Although there are previous versions, 4.0 was the first official version of the XML DocBook DTD released by the DocBook Technical Committee of OASIS.

> Quite frankly, when you start dealing with XML, SGML, and standards organizations, things become hideously complicated. Standards hinge on other standards; the documentation is jargon-filled and agonizing to read. The whole purpose of this book is to help you approach DocBook in a complete but user-friendly manner that negates the need to slog through documentation that would put an insomniac to sleep.

![](img/81f56bf497dbf7f7582072400d12cb42_25_0.png)

Now that you have whetted your appetite to learn more about DocBook, it's time to move on to the real thing. We hope that you enjoy using DocBook and find this book an easy read. If you have questions, comments, or concerns, feel free to write to Zonker at jbrockmeier@earthlink.net. He can't promise that he'll respond to all inquiries, but he promises that he will read them all.

## Chapter 1: Getting Started

### Creating DocBook Documents

### Understanding DocBook Markup

## Chapter 1: Getting Started

Now that all the introductory stuff is out of the way, it's time to get started with DocBook. The purpose of this chapter is to prepare you for writing DocBook documents. This chapter covers the major differences between SGML and XML Doc, how to use the DocBook DTD, and how to read DocBook markup so that it doesn't look like a foreign language. We'll also talk briefly about stylesheets, which are used to give a DocBook document its "look and feel."

Unlike the majority of this book, the material in this chapter is not used in the rest of the book. It might seem slow, so you might prefer to start with XML.

## Creating DocBook Documents

## SGML or XML?

The first thing to do is to choose which DTD is best for you. If you're going to be sharing documents with other organizations or companies that are using DocBook, the tools that they are using the SGML DTD and tools that are already available. If that's the case, you will want to stay the course and use the SGML DTD, unless you're willing to convert documentation to XML. This can be more trouble than it's worth, unless you need features provided by XML.

On the other hand, if you're using DocBook for the first time and you're going to be setting a standard, XML is probably the way to go. XML is one of today's technologies and it looks as though XML is capturing the hearts and minds of IT professionals in a way that SGML never did.

As of DocBook version 4.0, there are two official versions of the DTD: the SGML DTD and the XML DTD. The XML DTD has been around for a while, but the 4.0 version of the XML DTD was the first official release of DocBook.

It's likely that there will soon be an official XML Schema for DocBook as well. Chapter 11 covers XML Schemas in detail, though they aren't used in examples throughout the book. The reason for this is that the first experimental DocBook Schema was only recently introduced. However, Chapter 11 added because I felt that the topic should not be ignored and XML Schemas are likely to play an important role in DocBook development of the future.

![](img/81f56bf497dbf7f7582072400d12cb42_28_0.png)

XML is designed from the ground up for use on the Web. Using XML opens up the possibility of using DocBook documents for more than just standard publishing.
