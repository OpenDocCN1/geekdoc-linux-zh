# Creating DocBook Documents

The DOCTYPE declaration should be the first tag in every DocBook document. SGML requires this element so that any parsing application can identify the type of document it is working with and what DTD it is going to validate the document.

The DOCTYPE tag is followed by attributes that further define the type of document, including the DTD and the root element of the document.

# The Root Element

When you think of a root, what do you picture? What the designers of SGML want you to picture is a structure similar to a tree. The root element, like the roots of a tree, is the beginning of a structure. The root element is the foundation of the document. You can find all the valid root element types in Appendix B, "DocBook Element Reference."

# Public and System Identifiers

To use a DTD, an application must be able to find it. If a document has a public DTD, the application looks to a catalog file to resolve the name of the DTD to find the actual file, in this case:

```
// ANSI//DocBook V4.1//EN
```

On this system would resolve

```
/usr/share/sgml/dtd/docbook/4.1/docbook.dtd
```

By declaring a system identifier, you bypass the need to lookup a catalog file and simply tell the application exactly the file containing the DTD. If I use a system identifier instead of a public identifier, my declaration would look like this:

```
<DOCTYPE root element SYSTEM "/usr/share/sgml/dtd/docbook/4.1/docbook.dtd">
```

If you prefer, you can use both public and system identifier, but you must use at least one of them. Chapter 6, "Parsing DocBook," goes into more detail about the jaunty-gritty details of using DTDs.

# Using the XML DTD

Technically, as mentioned earlier, XML documents do not require a DTD. However, because you're working with a specific DTD (DocBook), you will

![](bbox=[0.815, 0.105, 0.955, 0.145])

You might be wondering what it means to say that document is parsed. Originally, parse was a linguistic term for dividing words or phrases into components and analyzing them. If you have been studying grammar school, you were parsing the sentences. The same is true in computer applications. Applications download the document into component parts for further processing. For instance, it has to parse HTML document before it can display the document in human-readable format. A parsing application forms validation, which is to say it also checks whether your document conforms to the DTD and is properly structured.