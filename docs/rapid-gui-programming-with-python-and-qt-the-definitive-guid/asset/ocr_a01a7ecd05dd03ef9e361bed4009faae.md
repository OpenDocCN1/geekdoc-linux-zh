Earlier we mentioned that a QDomDocument could easily be written to a file. Here is how we could do it, assuming that dom is a QDomDocument and filename is a valid filename, but with no error checking:

```
codes.open(filename, "w", "utf-8").write(unicode(dom.toString()))
```

This will produce a file that is slightly different from the one produced by the exportXml() method. For example, the QDomDocument.toString() method indents nested tags, uses double quotes rather than single quotes for attributes, and may order the attributes differently. Nonetheless, the XML document produced is canonically identical to the one produced by exportXml().

Once the QDomDocument has read in the XML file we need to traverse its contents to populate the application's data structures, and to do this we begin by calling populateFromDOM() on the document.

```
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
```

We start by checking that the XML file we read is indeed a movies XML file. If it is not we raise an exception, and if it is, we clear our data structures so that they are ready to be populated by the data extracted from the DOM document.

DOM documents are composed of “nodes”, each of which represents an XML tag or the text between tags. A node may have children and it may have siblings. In the case of the movies XML format, we have sibling <MOVIE> nodes that have <TITLE> and <NOTES> child nodes, and these child nodes in turn have child text nodes. So to extract our data we iterate over the <MOVIE> nodes, and for each one we encounter, we extract its attributes and the data from its child nodes.

```
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
```