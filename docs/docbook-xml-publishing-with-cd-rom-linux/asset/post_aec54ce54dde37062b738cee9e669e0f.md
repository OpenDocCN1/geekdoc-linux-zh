
# Chapter 10: Customizing DocBook

## The DocBook Driver

The first version of DocBook, 1.0, was just one lone DTD. It contained everything that you need to know about DocBook and was easy to read on its own.

The current version of DocBook is split into separate files to make it easier to maintain. The main file is docbook.dtd which calls the rest of the files that make up the DocBook DTD when processed.

![](img/81f56bf497dbf7f7582072400d12cb42_231_0.png)

The rest of the files are modules that contain bits of DocBook, as well as the SGML entity sets. The entity sets are part of DocBook, but they are required and called from the DocBook DTD.

The Formal Public Identifier identified in the document declaration. It is the part of the declaration that identifies the owner of the DTD, and a description of it, and what line gauges it in. For example: //-// DTD DocBook V4.1//EN is not a DocBook-specific contingency; the FPI is part of the ISO standard.

## The Exception to the Rule

One file distributed with the DocBook DTD is kosher to modify without making a change in the DocBook Formal Public Identifier (FPI). That's the general entities module, dbgenent.mod.

Say that you want to add an entity like your company name or program to the entities you're fed up typing Global Mega Corporation Central Division Office or something equally RSI-inducing (Repetitive Strain Injury).

The file you modify is the dbgenent.mod file. It is designed to have extra entities added to it. To add an entity, open the file and add a line like:

```
<ENTITY companyname "Global Mega Corporation Central Division Office">
```

Then, any time you type &companyname;, it will automatically be expanded to Global Mega Corporation Central Division Office, and you will save your self from RSI.

## The Table DTD

The CALS Table model is one of the files distributed with DocBook as cals-tbl.dtd. This is the DTD that describes table markup that DocBook uses. It is not a product of the DocBook Technical Committee. The CALS Table model was created by the United States of Defense as a standard for the exchange of electronic data between commercial suppliers.

## DocBook Elements

The majority of DocBook elements are declared in the DocBook Information Pool-module, dbpool.mod. This file contains most of the objects and elements used in DocBook. As mentioned previously, the table elements are declared elsewhere. The DocBook structural elements are also contained in a separate file, which you will get to in the next section.

Although I don't recommend making any modifications to the file, it is instructive to take a look at it. The Trademark element—not one of the most complicated elements but not the simplest—has a few nonstandard attributes, so have a look at it to see what a typical element declaration looks like:

```
<!ENTITY % trademark.module INCLUDE>
[ % trademark.module;
<!ENTITY % local.trademark.attrib " ">\n<!ENTITY % trademark.role.attrib "%role.attrib;">
]
<!!ENTITY % trademark.element INCLUDE>
[ % trademark.element;
<!ELEMENT Trademark - ((#PCDATA
  |link.char.class;
  |tech.char.class;
  |base.char.class;
  |other.char.class;
  |InlineGraphic
  |InlineMediaObject
  |Emphasis))+>
<!---end of trademark.element->]>
```

```
<!ENTITY % trademark.attlist INCLUDE>
[ % trademark.attlist;
<!ATTLIST Trademark
```

Class: More precisely identifies the item element names

| Class | Service |
| --- | --- |
| Trade | Registered |
| Copyright | Trade %common.attrib; %trademark.role.attrib; %local.trademark.attrib; |

```
<-end of trademark.attlist->>
<-end of trademark.module->
```

That probably looks confusing, but it's just verbose. I will break it down so that it makes more sense.

```
<!ENTITY trademark.module "INCLUDE">
[: %trademark.module; [
<!ENTITY local.trademark.attrib "%role.attrib;">
```

This is the Entity declaration, which tells the parser that there is an entity named Trademark and that it should be included. The third and fourth lines are declaring an attribute for the Trademark element. The next lines let the parser know which elements can occur as child-elements of the Trademark element. Some elements are declared as groups, such as the tech group of elements. Other elements, such as InlineGraphic, are explicitly declared. The final section of the Trademark declaration defines the attributes for Trademark, including acceptable values for the Class attribute. The practical use of all this information is for Jade, or whatever parsing tool you're using, can give you an error message like the one in Figure 10.1 should you use an invalid attribute. As you can see in Figure 10.1, the DocBook DTD is intricate. It's not that this stuff is complicated, certainly no more difficult than speaking English. However, as we know, the English language is made up of many rules to understand before you can speak intelligently. When you write a DTD, it's very similar to creating a language, so if you attempt to alter the language you have to be very careful.

## The DocBook Hierarchy

Although most elements in DocBook are contained in the Information Pool module, dbpool.mod, all the hierarchical elements in DocBook are contained in the hierarchy module, dbhier.mod. If you want to get information on any hierarchical elements in DocBook, such as the Section or the Book element, look in this file. The structure and syntax of the file are the same as the others, but for organizational purposes, the DocBook Technical Committee has segregated hierarchical content into this file.

## Customizing the DocBook DTD

![](img/81f56bf497dbf7f7582072400d12cb42_234_0.png)

Figure 10.1 Jade's error for an invalid attribute

## The DocBook Character Entities

The DocBook Character Entities file is dbent.mod. This file doesn't contain much information directly; rather it calls the various files that have ISO character entities. If you don't have the ISO entities on your system when you parse a DocBook document, you will get a whole bunch of errors.

## The DocBook Catalog

All the DocBook information is contained in the docbook.cat for use in building your own catalog files. The information here can be useful in debugging if you have Jade/OpenJade errors related to catalog files.

## DocBook SGML Declarations

The docbook.dtd file contains all of DocBook's SGML declarations. When you see errors like the one in Figure 10.2, which complain about a missing tag but its declaration does not permit this, this is where the declaration to omit tags is located.

```
book-patron:/Writing/Prima/SQL$ tools -b html Test.m
/usr/bin/jade:OSD:016:409:E: end tag for "ACRONYM" omitted, but its declaration does net syntax error
/usr/bin/jade:OSD:016:300: start tag was here
book-patron:/Writing/Prima/SQL$ $
```

![](img/81f56bf497dbf7f7582072400d12cb42_235_0.png)

Figure 10.2 A Jade error

## DocBook Notations

The dbnot.mod file contains the notations for DocBook. This includes references to most types of binary graphics files.

## Customizing Stylesheets

If you want to get a different look and feel out of DocBook, it isn't necessary to change the DTD in any way. The look and feel of your output is determined by the stylesheet, not the DTD, as mentioned earlier.

The nice thing about DocBook is that it allows separation of structure and content from display. In fact, DocBook makes it easier to display the same information in different ways without reformatting any of the document itself. Simply by switching the stylesheets, you can completely change the look or medium of the output. This is one area where DocBook has an advantage over GUI tools such as Microsoft Word. Although Word does a multitude of nifty reformats, it isn't possible to write a document in Word and have it completely reformat your document by the type of information contained in it. For instance, with DocBook, you can create a stylesheet that displays information contained only in the Author and Editor elements. Word would be stumpied by this request because it doesn't distinguish the content in a document that way.

> It's my pet theory that all these years, Microsoft Word contains at least one feature no one has ever used and several features about the majority of folks working on Word have no idea.

![](img/81f56bf497dbf7f7582072400d12cb42_236_0.png)

## Understanding DSSSL

Okay, you're probably looking at the acronym and thinking that it has to be really hard to read an FLA (Five-Letter Acronym) instead of the standard TLA (Three-Letter Acronym). Don't worry, the Document Style Semantics and Specification Language isn't any worse than other technologies you've looked at. It just has a verbose title.

DSSSL is a style language. It's a derivative of the Scheme and Lisp programming languages, which is why it has so many parentheses.

> An older programmer I used to know once that Lisp should actually stand for Lots of Insidious Parentheses. If you program in Lisp, you will find yourself touch-typing the parenthesis key, if nothing else.

![](img/81f56bf497dbf7f7582072400d12cb42_236_1.png)

A full overview of DSSSL is well beyond the scope of this book. DSSSL is a very full-featured language. However, I will provide a few examples of customizing a stylesheet to get you started.

## Making Changes to Existing Stylesheets

Usually, it's better to make changes to existing stylesheets than to try to write them from scratch. Remember, DocBook has more than 300 elements, and you don't want to be writing a stylesheet from scratch to support more than 300 elements and their attributes.
