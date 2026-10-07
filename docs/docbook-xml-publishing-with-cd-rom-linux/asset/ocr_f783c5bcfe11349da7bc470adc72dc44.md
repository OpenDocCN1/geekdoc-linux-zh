# Differences between SGML and XML DocBook

SGML and XML DTDs are designed to be fully compatible. However, SGML allows some shortcuts—better known as minimization—that are not allowed in XML. Because the goal of this book is to bring you up to speed with both SGML and XML DocBook, I won't demonstrate any of the minimizations in this book. No need to start bad habits!

Another difference between SGML and XML is case-sensitivity. SGML allows for uppercase, lowercase, and mixed-case elements and attributes. <Sect>, <sect1>, and <sect> are all valid markup when working with SGML, but only lowercase elements and attributes are valid with the DocBook XML DTD. The reason for this is that XML is designed so that a well-formed XML document can be parsed without a DTD. Even there is a DTD for XML DocBook, XML tools should be able to work with a DocBook XML document without a DTD.

> The SGML specification from the W3C does not require elements to be lowercase, but it does require that elements used as they are defined in the DTD. The DocBook DTD defines all elements in lowercase for simplicity.

Keywords, on the other hand, must be uppercase to be considered valid with XML. If this seems confusing, don't worry. If you follow the conventions and examples in this book, you'll be fine. All the examples in the book have been designed to be XML and SGML DTD compatible. Remember, valid XML is also valid SGML, but the reverse is not true. Designing documents to be compatible with both, even if you are using the SGML DTDs now, can save you headaches later.

When you have settled on SGML or XML, you will start your document with one of the declarations.

# Using the SGML DTD

To declare a document using the SGML DTD, use the following markup:

```
<DOCTYPE root element PUBLIC "-//OASIS//DTD DocBook V4.1//EN">
```

I'll break this down into the basic components so that it's easier to understand.

![](bbox=[0.053, 0.436, 0.163, 0.676])

+   In a DocBook document, keywords are used to designate sections that should receive special handling. For instance, the CDATA keyword is used to indicate that within a certain section marked should not be processed.