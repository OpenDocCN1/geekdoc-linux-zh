# Chapter 4: Preparing a Book with DocBook

&chapter2;
&chapter3;
&chapter4;
&index;
&glossary;
&appendix;
&bibliography;
&</book>

That is a valid declaration for an SGML DocBook Book. Note that it doesn't contain any text within the book itself.

To break it down, the first line is the document declaration itself. Here, you're telling any application that is going to parse the file, which type of document this is, and what to expect. The following lines, enclosed in brackets and beginning with <ENTITY, declaring entities for the parser. These are not DocBook entities; they are entities that refer to files on your system. This allows you to refer to the entities under the Book element enclosing

![](bbox=[0.181, 0.473, 0.93, 0.843])

```
<!DOCTYPE book PUBLIC "-//DTD//DocBook V4.1//EN// >
  <!ENTITY preface SYSTEM "preface.sgml">
  <!ENTITY chapter1 SYSTEM "chapter1.sgml">
  <!ENTITY chapter2 SYSTEM "chapter2.sgml">
  <!ENTITY chapter3 SYSTEM "chapter3.sgml">
  <!ENTITY index SYSTEM "index.sgml">
  <!ENTITY glossary SYSTEM "glossary.sgml">
  <!ENTITY appendix SYSTEM "appendix.sgml">
  <!ENTITY bibliography SYSTEM "bibliography.sgml">
```

figure 4.2 The Book declaration in Vim