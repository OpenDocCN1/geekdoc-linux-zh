
## How Does a Schema Differ from a DTD?

<para>
<alink url="http://www.w3.org/"><cite>World Wide Web Consortium</cite></alink>. This is an example of a URI in a document. The URL attribute of the Ulink element contains a valid URI.
</para>

![](img/81f56bf497dbf7f7582072400d12cb42_248_0.png)

Figure 11.2 An example of a URI in a document

# Reference

Another important data type that doesn't quite fit in the string or CDATA data types is the URL. If you recall, URIs are the Uniform Resource Identifiers. These are very important to DocBook and XML. The XML Schema specification allows for a URIReference type, which can contain a URI or URL. Figure 11.2 shows a URI in a document.

There are a number of other data types, too numerous to discuss here. However, you must understand that data typing is very important to XML Schema. When the XML DocBook Schema becomes more commonly used, it will be necessary to understand which data types you can use with each element.

# Elements and Attributes

Elements and attributes behave mostly as they do with a DTD. You use elements to define the data contained within them and attributes to further define the element.

# Chapter 11: XML Schema and DocBook

However, in XML Schema some elements are not allowed to contain attributes. Elements that have a simple data type (such as the decimal data type) are, by definition, not supposed to contain attributes.

This is different from the DTD and from what you might be used to already with DocBook. All elements in DocBook may contain attributes.

# Defining an Element

How do you know which an element can contain? It's within the Schema specification for the element. Take a quick look at reading the element definition from an imaginary Schema that defines a simple element.

You will specify a simple element first, and then you will specify a few more complex elements to get the full picture. The first element is the Para element containing any data that can be in a paragraph.

```
<xsd:schema xmlns:xsd="http://www.w3.org/2000/08/XMLSchema">
<xsd:annotation>
<xsd:documentation>
This is a sample documentation
</xsd:documentation>
</xsd:annotation>
<xsd:element name="para" type="CDATA"/>
</xsd:schema>
```

The first thing you might have noticed is the format—each part of the Schema declaration begins with <xsd:, which stands for Schema declaration.

Another thing you might have noticed is the annotation and documentation elements. XML Schema allows for documentation of itself as it goes along. This means that when writing a Schema, the author of the Schema can add documentation explaining the elements that are defined as they are included. This is exciting because it allows for self-generating documentation. Simply run the Schema through a parser with the proper stylesheet, and it can generate its own documentation. Nifty, isn't it?

Finally, the element declaration itself is simple. The <xsd:element markup lets you know that you are declaring an element. The Name attribute tells you the name the element will have, and the Type attribute defines the type of data the element can have. Because you want to allow just about anything in the Paragraph element, you specify the CDATA data type, covered earlier in the chapter.

Now for a slightly complex set of elements. This example defines an element containing two other elements. Note that the top-level element itself contains only other elements, not data.

```
<xsd:schema xmlns:xsd="http://www.w3.org/2001/08/xml-schema">
<xsd:annotation>
<xsd:documentation>
This is a sample Schema for more complex elements.
</xsd:documentation>
</xsd:annotation>
<xsd:complexType name="ComplexElement">
<xsd:sequence>
<xsd:element name="SimpleElement1" type="xsd:string"/>
<xsd:element name="SimpleElement2" type="xsd:decimal"/>
</xsd:sequence>
</xsd:complexType>
<!-- This is a comment -->
</xsd:schema>
```

As you look at this example, you will notice that the format is basically the same. However, the ComplexType element contains an xsd:sequence that defines the sequence of elements contained within the Complex element. If you see a MinOccurs or MaxOccurs attribute, you know that the elements must occur within the Complex element a specific number of times or the document will not be valid within the Schema.

Note that even within the XML Schema documents, HTML-style comments are valid.

The purpose of this section is not to get started on writing your own Schema. Norman Walsh and the DocBook Technical Committee will be doing that. However, you might have to read an XML Schema to make use of the DocBook XML Schema as it enters widespread usage.

# The DocBook XML Schema

The DocBook XML Schema is not yet final and isn't ready for production use at the time of this writing. Furthermore, none of the tools that you used to process DocBook are geared to utilize the Schema for DocBook.

The first (alpha) release of the DocBook XML Schema was announced on November 8, 2000, to the DocBook mailing list. Not much documentation

# Chapter 11: XML Schema and DocBook XML

exists yet for the DocBook Schema, nor are there any tools for working with the Schema. However, it's valuable to follow the development and be ready for using the Schema.

# The DocBook XML Schema

The DocBook XML Schema is not yet final and isn't ready for production use at the time of this writing. Furthermore, none of the tools that you used to process DocBook are geared to utilize the Schema for DocBook.

The first (alpha) release of the DocBook XML Schema was announced on November 8, 2000, to the DocBook mailing list. Not much documentation

exists yet for the DocBook Schema, nor are there any tools for working with the Schema. However, it's valuable to follow the development and be ready for using the Schema.

# Validating the XML

If you're trying to validate documents, you can use the Schema. There are many tools available for this, but for now, you might have to use the online tools at http://w3.org/2000/see 11.3.

![](img/81f56bf497dbf7f7582072400d12cb42_251_0.png)

Figure 11.3 The DocBook Schema

![](img/81f56bf497dbf7f7582072400d12cb42_252_0.png)

Figure 11.4 The X validator

# Summary

In this chapter you've looked at the XML Schema and how it relates to DocBook. Although Schema is still in its developmental stage, it is likely to become very important as XML picks up.

If you're deploying DocBook XML, you will want to develop an understanding of the Schema. The DocBook XML Schema, in particular, is not currently in practical use, so for now you must stick with the DocBook DTD.

# Chapter 12: Creating Technical Documents

Corporate Documents

Making a Style Reference Page

Notes, Cautions, Tips, and Warnings

Fun with Errors

Writing about GUIs

Marking Up Command Syntax

Though DocBook is excellent for a lot of writing projects, it truly excels at technical documentation. This makes sense because that's where DocBook got its start. DocBook started as a markup language just for documentation of UNIX-type operating systems. It has changed considerably and gotten much flexible since then.

DocBook now has elements to describe hardware, databases, elements of a GUI, command syntax, and more. This chapter demonstrates some of the DocBook elements that are particularly useful for marking up technical documents. Using the right elements will make your documents much easier to read, especially when you need to include code samples.

This chapter will also briefly cover some elements that describe meta-information you might run into when working on a technical document for your employer or when writing a document for presentation. You're on your own when it comes to actually delivering the presentation. Speaking still gives me the jitters, despite the well-intentioned advice, picturing an audience of geeks neked is not a good idea.

## Corporate Documents

Many technical documents written for large companies are credited with corporate authorship instead of being attributed to a single author.

To include corporate authorship information in a document, you use the CorpAuthor element in the meta-information for the document. For example, if you were preparing an article with DocBook, the markup would look like this:

```
<DOCTYPE article PUBLIC "//ASIS//DTD DocBook V4.1//EN">
<article>
<articleinfo>
<title>A Technical Manual</title>
<corporauthor>Mega-big Corporation</corporauthor>
</articleinfo>
..
</article>
```

Note that the ArticleInfo element is new with DocBook 4.0. If you are still maintaining documents from DocBook 3.0, you'll find the same information in the ArtHeader element, which is now deprecated.
