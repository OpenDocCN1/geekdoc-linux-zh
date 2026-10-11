# Listing 3. Extracting files for the ODT Archive

```
```python
import sys, zipfile
if len(sys.argv) < 2:
    print 'Usage: extract odf-filename outputfilename
    sys.exit(0)

myfile = zipfile.ZipFile(sys.argv[1])
listoffiles = myfile.infolist()
for s in listoffiles:
    if s.orig_filename == 'META-INF/manifest.xml':
        fd = open(sys.argv[2], 'w')
        bh = myfile.read(s.orig_filename)
        fd.write(bh)
        fd.close()
```
```

disk as an independent file. Listing 3 shows how to extract the manifest.xml file.

For more than one file, you can use a list instead of the if clause:

```
```python
if s.orig_filename in ['content.xml', 'styles.xml']:
```
```

This way, you can extract whatever files you need to look at simply by reading in their contents and either manipulating them or writing them off to disk.

The contents of an XML file are best suited for manipulation as a tree structure. Use the XML parsing capabilities in Python to get a tree of all the nodes within an XML file. Once you have the tree in a content file, you easily can get to the `<text:p>` nodes. You don't really have to extract the file to disk, because you also can run an XML parser on the string just as well as reading from a file.

There are two types of XML parsers, SAX and DOM. The SAX parser is faster but less memory-intensive, because it reads and parses an input file one tag at a time. You can only one tag at a time to work with and must track data yourself. In contrast, the DOM parser reads the entire file into memory and therefore provides better options for navigating and manipulating the XML nodes.

Let's look at examples of using both SAX and DOM, so you can see which one suits your purpose. The SAX example shows how to extract unique node names from an XML file. The DOM example illustrates how to read values from within specific nodes once the file has been read completely into memory.

First, let's use the SAX parser to see what node are available in the content.xml file. The code simply prints the name of each type node found in the file. Note that for different types of files you may get different node names (see Listing 4).

A SAX program requires a class derived from `ContentHandler` and overriding functions to handle the start, middle and end of each node. The `tagHandler` class shown in Listing 4 is used primarily to track the start of each node and ignore the contents. Here use the `keys()` method to list the names into a list that you also can sort(). I use this technique quite often to get a sorting of unique members quickly, because the hashing functions in Python dicto-

# Listing 4. List uniq Tag Numbers

```
```python
#
# This program will list out the uniq tag
# names in a XML document.
# Author: Kamran Mousin
#

import sys
from xml.sax import parse, ContentHandler

class tagHandler(ContentHandler):
    def __init__(self, tagname = None):
        self.tag = tagname
        self.uniq = {}

    def startElement(self, name, atr):
        if self.tag == None:
            self.uniq[name] = 1;
        elif self.tag == name:
            self.uniq[name] = name
            # ignore attributes for now

    def getNames(self):
        return self.uniq.keys()

if __name__ == '__main__':
    mytagHandler = tagHandler()
    parse(sys.argv[1], mytagHandler)
    myNames = [str(x) for x in mytagHandler.getNames()]
    myNames.sort()
    for x in myNames: print x
```
```

naries are very fast. Here's the output from the program:

+   - office:automatic-styles
+   - office:styles
+   - office:document-content
+   - office:font-face-decls
+   - office:forms
+   - office:text
+   - style:font-face
+   - style:list-level-properties
+   - style:paragraph-properties
+   - style:style
+   - style:text-properties
+   - text:a
+   - text:line-break
+   - text:list
+   - text:list-item
+   - text:list-level-style-bullet
+   - text:list-style
+   - text:p
+   - text:s
+   - text:sequence-decl