# Linking within a Document

One of the most useful features in HTML is your ability to create relative links within a document to other portions of the document. DocBook markup also enables you to create links within your document to other portions of your document, but they're not straightforward as the system used in HTML markup.

In HTML you can simply use an anchor element for both the link and the target. The XRef attribute for the Anchor element generates the link, and the Name attribute provides a target for the link. In DocBook markup, you can use several elements to generate internal links.

The elements used for links within a document are Anchor, Link, and XRef. XRef is capable of doing more than just generating a link to other text, however. With the XRef element, you can also pull text from other DocBook elements. For instance, you can use the Title attribute from the Chapter element. The XRef element uses the ID attribute from other elements.

The Anchor element is used to provide a reference point for the XRef element when another element with an ID attribute to link to not exist.

> Remember, when using an ID attribute, it must be unique within the document. you can use chapter2 and chapter3 as values for the ID attribute for two consecutive chapters, preferably Chapters 2 and 3, but you would not use the value chapter twice.

Although the ID attribute must be unique, there can be multiple pointers to one ID—for example, if you have this markup:

```
<chapter id="introduction">
<title>Introduction</title>
</chapter>
```

You can have this markup at the end of every other chapter:

```
<para>
<xref linkend="introduction">
</para>
```

which would generate a link to the beginning of the Introduction.

![](bbox=[0.075, 0.735, 0.175, 0.935])