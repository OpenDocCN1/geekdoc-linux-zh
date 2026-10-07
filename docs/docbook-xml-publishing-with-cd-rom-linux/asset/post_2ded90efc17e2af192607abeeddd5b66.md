
## Chapter 5: Making Online Documents

Figure 5.1 shows what the ULink looks like after being rendered into HTML using the default stylesheets. However, the information is not lost in print publications. Figure 5.2 shows the DocBook markup output to PostScript.

Obviously, you can't click on a link in a paper document and go to a Web site. However, the URL for the site is neatly printed next to the title of the site so it can be manually entered if the reader wishes.

The ULink element can also be used for linking to files on an FTP server to an Archie or Gopher server—it could also be used for protocols that don't exist yet.

To give another example, maybe your document link should link to an FTP server to retrieve extra documentation (see Figure 5.3). The syntax is such as:

```
<para>
You can find supplemental documentation at this FTP site:
<ulink url="http://yourserver.net/documents/extra.sgml">
<title>http://yourserver.net/documents/extra.sgml</title>
</ulink>
</para>
```

![](img/81f56bf497dbf7f7582072400d12cb42_123_0.png)

## Chapter 1. ULink Element

The offset is/DocBook Website
This is an example of an ULink element in DocBook.

Figure 5.1 A link from DocBook in HTML

## Chapter 1. ULink Element

1.1.

The Official DocBook Website (http://www.casi-open.org/docbook/)
This is an example of an ULink element in DocBook.

Figure 5.2 PostScript output

![](img/81f56bf497dbf7f7582072400d12cb42_124_0.png)

You can find supplemental documentation at this FTP site:
http://ftp.yourserver.net/documents/extra.sgml

Figure 5.3 Linking to an FTP server

![](img/81f56bf497dbf7f7582072400d12cb42_124_1.png)

## Linking within a Document

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

![](img/81f56bf497dbf7f7582072400d12cb42_125_0.png)

## Creating Online Documentation

## How XRef Works

XRef pulls the information needed from the ID attribute and the Title element, or if the element does not contain a child element, it uses the RefLabel attribute. If an element does not support the Title element or the RefLabel attribute, you must use the Anchor element, which can be located virtually anywhere within a document, as long as it is nested within one of its parent elements.

Your head swimming from jargon? Are child and parent elements confusing you? If you skipped the Introduction, now might be a good time to backtrack and skim through it. You can also check out Appendix A, "DocBook Glossary," if you are just a little fuzzy on the terms.

If you feel confused, don't think you're alone: DocBook was not created with user-friendliness. The concepts behind DocBook are not impossible to get handle on, it might help to take a breather and absorb what you've covered.

DocBook markup is literally another language, admittedly a limited one based on English. Everyone knows that it takes patience and time to pick up the same goes for DocBook. The downside to DocBook, compared with real languages, is that there's nowhere you can go to immerse yourself in the language, and there's no native cuisine for DocBook—unless you count native elements as chapters and sections.

![](img/81f56bf497dbf7f7582072400d12cb42_126_0.png)

**NOTE**

To use XRef to link to a section within your document, do something like this:

```
<section id="xref">
  <title>Using XRef</title>
</section>
<xref linkend="xref"/>
```

## Chapter 5: Making Online Documents

![](img/81f56bf497dbf7f7582072400d12cb42_127_0.png)

Figure 5.4 An XRef link

The linkend attribute value that is called by the XRef element will correspond to the ID value when the document is parsed. If you are creating an HTML document, you will get output like that shown in Figure 5.4.

Note that the XRef element is an empty element. If you were using the DocBook XML DTD, you would use this markup for the XRef element:

```
<xref linkend="xref"/>
```

The only difference in the markup is the closing character. However, it will cause errors if the character is missing. If you're rendering your document in PostScript, or other print formats, your markup will look like that shown in Figure 5.5.

## Using the Anchor Element

Note that unlike a link in HTML, you do not have to supply the descriptive text for the link—the text is derived from the Title element instead. If you're using the XRef element, you supply the descriptive text for the link with the RefLabel attribute.

## Creating Online Documentation

![](img/81f56bf497dbf7f7582072400d12cb42_128_0.png)

Figure 5.5 XRef output in static text

> Note that the Anchor element in DocBook markup (<anchor>) and the Anchor element in HTML (<a>) are completely different and do not use the same syntax. Although they have the same purpose, generating hyperlinks and references, they do not bear much relation.

To use the Anchor element, use the following syntax:

```
<para>
This is an example of the <anchor id="xref.example" label="XRef Example">XRef and Anchor elements.</
</para>
```

The Anchor element is also an empty element. If used with the XML DTD, you must be sure to close the element with the character, like this:

```
<anchor id="xref.example" label="XRef Example"/>
```

You might have noticed another trick I introduced with the ID attribute in the example. Earlier, you started a section element with the ID attribute value

## Chapter 5: Making Online Documents

xref, which you can't use again in the document because it will cause parsing problems.

However, because you are probably writing an entire section about the XRef element, you want to use ID values that relate to the topic they describe—just as you would use descriptive variable names when programming, you want to use descriptive names in your ID attribute values.

Because I couldn't reuse xref, I used xref.example, which is perfectly valid because it is also unique within the document. If you're writing an entire section on a particular topic, I would suggest using a simple descriptor like xref for the ID value of the top-level of the document hierarchy and then using derivatives of that value for the rest of the section. This helps as your documents become more and more complex, if you use values that are easy to remember and flow logically. I would not recommend simply using chapter or sections or any type of numbering scheme. If you become dependent on a numbering scheme, you will find yourself redoing a lot of markup when you add an extra section or otherwise revise the document. Remember that the ID attribute's values are not seen within the finished documents, so you can be relatively verbose and descriptive with your ID values.

## Using the Link Element

The Link element behaves more like the Anchor element from HTML markup than the other linking elements used in DocBook. The Link element is used in a similar fashion to the XRef element, but it is not an empty element. This can be useful if you want to link to something with a Title element but do not want to use that title for the link text.

The syntax of the Link element is as follows:

```
<section id="link">
<title>Using Link Elements</title>
<para>
Some Web sites, <link linkend="website">like this one</link>, are examples of excellent Web design.
</para>
</section>
<section id="website">
<title>Themes.org</title>
<para>
```
