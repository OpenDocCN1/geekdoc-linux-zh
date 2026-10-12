
## Reading and Parsing XML with PyQt’s DOM Classes

PyQt’s QDomDocument class can be used to read in an entire (well-formed) XML document in one go. But once we have a QDomDocument, we must be able to use it. Some applications reflect the document into a widget, often a QTreeWidget, whereas others, like My Movies, which use XML purely as a data-interchange format, traverse the document, populating their data structures as they go.

```python
def importDOM(self, fname):
    dom = QDomDocument()
    error = None
    fh = None
    try:
        fh = QFile(fname)
        if not fh.open(QIODevice.ReadOnly):
            raise IOError, unicode(fh.errorString())
        if not dom.setContent(fh):
            raise ValueError, "could not parse XML"
    except (IOError, OSError, ValueError), e:
        error = "Failed to import: %s" % e
    finally:
        if fh is not None:
            fh.close()
            if error is not None:
                return False, error
    try:
        self.populateFromDOM(dom)
    except ValueError, e:
        return False, "Failed to import: %s" % e
    self.__fname = QString()
    self.__dirty = True
    return True, "Imported %d movie records from %s" % (
        len(self.__movies), QFileInfo(fname).fileName())
```

The first part of the load method should appear familiar, but notice that the entire file is read when we call QDomDocument.setContent(). If this method succeeds (returns True), we know that the XML was successfully parsed.

Once we have a QDomDocument, we need to extract our data from it, and that is what the populateFromDOM() method does.

The end of the method is different from what we have seen before. We clear the filename and set the dirty flag to True. This will ensure that if the user tries to save the XML movie data they have just imported, or if they try to quit the application, they will be given a “save as” dialog so that they get the chance to save the data in one of the application’s binary or text formats.

Earlier we mentioned that a QDomDocument could easily be written to a file. Here is how we could do it, assuming that dom is a QDomDocument and filename is a valid filename, but with no error checking:

```python
open(filename, "w", "utf-8").write(unicode(dom.toString()))
```

This will produce a file that is slightly different from the one produced by the exportXml() method. For example, the QDomDocument.toString() method indents nested tags, uses double quotes rather than single quotes for attributes, and may order the attributes differently. Nonetheless, the XML document produced is canonically identical to the one produced by exportXml().

Once the QDomDocument has read in the XML file we need to traverse its contents to populate the application's data structures, and to do this we begin by calling populateFromDOM() on the document.

```python
def populateFromDOM(self, dom):
    root = dom.documentElement()
    if root.tagName() != "MOVIES":
        raise ValueError, "not a Movies XML file"
    self.clear(False)
    node = root.firstChild()
    while not node.isNull():
        if node.toElement().tagName() == "MOVIE":
            self.readMovieNode(node.toElement())
        node = node.nextSibling()
```

We start by checking that the XML file we read is indeed a movies XML file. If it is not we raise an exception, and if it is, we clear our data structures so that they are ready to be populated by the data extracted from the DOM document.

DOM documents are composed of “nodes”, each of which represents an XML tag or the text between tags. A node may have children and it may have siblings. In the case of the movies XML format, we have sibling <MOVIE> nodes that have <TITLE> and <NOTES> child nodes, and these child nodes in turn have child text nodes. So to extract our data we iterate over the <MOVIE> nodes, and for each one we encounter, we extract its attributes and the data from its child nodes.

```python
def readMovieNode(self, element):
    def getText(node):
        child = node.firstChild()
        text = QString()
        while not child.isNull():
            if child.nodeType() == QDomNode.TextNode:
                text += child.toText().data()
            child = child.nextSibling()
        return text.trimmed()
```

The readMovieNode() begins with a nested function definition. The getText() function takes a node as an argument—for example, a <TITLE> or <NOTES> opening tag—and iterates over its child text nodes, accumulating their text. Finally, it returns the text, with whitespace stripped from either end. As noted earlier, the QString.trimmed() method does the same job as unicode.strip().

```python
year   = intFromQStr(element.attribute("YEAR"))
minutes = intFromQStr(element.attribute("MINUTES"))
ymd = element.attribute("ACQUIRED").split("-")
if ymd.count() != 3:
    raise ValueError, "invalid acquired date %s" % \
        unicode(element.attribute("ACQUIRED"))
acquired = QDate(intFromQStr(ymd[0]), intFromQStr(ymd[1]),
                 intFromQStr(ymd[2]))
```

The readMovieNode() method itself begins by extracting the <MOVIE> tag's attribute data and converting it from text into ints for the year and minutes, and into a QDate for the date acquired.

We could have avoided having to handle the details of the acquired date ourselves, and pushed the work onto the parser. For example, instead of having a single ACQUIRED attribute, we could have had ACQUIREDYEAR, ACQUIREDMONTH, and ACQUIREDAY, each with an integer value. With these three attributes we would not need to do the split on hyphens, but the format would have been more verbose.

```python
title = notes = None
node = element.firstChild()
while title is None or notes is None:
    if node.isNull():
        raise ValueError, "missing title or notes"
    if node.toElement().tagName() == "TITLE":
        title = getText(node)
    elif node.toElement().tagName() == "NOTES":
        notes = getText(node)
    node = node.nextSibling()
    if title.isEmpty():
        raise ValueError, "missing title"
self.add(Movie(title, year, minutes, acquired,
               decodedNewlines(notes)))
```

Each <MOVIE> node has two child nodes, <TITLE> and <NOTES>. Although we always write them in the same order in the exportXml() method, we don't want to force the child nodes to have a particular order. For this reason, we iterate over the child nodes and use the nested getText() method to gather the text for whichever child node we encounter.

At the end, providing the movie has a title, we create a new Movie object and immediately add it to our data structures using add().

Using a DOM parser for importing XML into custom data structures works fine, although we often need to write small helper functions like getText(). DOM is best used in situations where we want to hold and manipulate the XML data inside a QDomDocument itself, rather than converting it into other data structures.

## Reading and Parsing XML with PyQt’s SAX Classes

Importing XML using a SAX parser works quite differently than using a DOM parser. With SAX, we define a handler class that implements just the methods that we are interested in, and then give an instance of the handler to the SAX parser to use as it parses the XML. Parsing is not done in one go as it is with DOM, but rather piece by piece, with our handler’s methods being called when the data they handle is encountered. Any methods that we do not implement are provided by the base class, and in all cases they safely do nothing.

```python
def importSAX(self, fname):
    error = None
    fh = None
    try:
        handler = SaxMovieHandler(self)
        parser = QXmlSimpleReader()
        parser.setContentHandler(handler)
        parser.setErrorHandler(handler)
        fh = QFile(fname)
        input = QXmlInputSource(fh)
        self.clear(False)
        if not parser.parse(input):
            raise ValueError, handler.error
    except (IOError, OSError, ValueError), e:
        error = "Failed to import: %s" % e
    finally:
        if fh is not None:
            fh.close()
        if error is not None:
            return False, error
        self.__name = QString()
        self.__dirty = True
        return True, "Imported %d movie records from %s" % (
            len(self.__movies), QFileInfo(fname).fileName())
```

We begin by creating an instance of a custom SaxMovieHandler and of a SAX XML parser. The parser can be given a content handler, an error handler, and some both handlers; we have chosen to create just one handler, one that can handle both content and errors, so we set this same handler for these two purposes.
