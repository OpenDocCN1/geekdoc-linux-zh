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

Finally, the element declaration itself is simple. The <xsd:element markup lets you know that you are declaring an element. The Name attribute tells you the name the element will have, and the Type attribute defines the type of data the element can have. Because you want to allow just about anything in the Paragraph element, you specify the CDATA data type, covered earlier in the chapter. **