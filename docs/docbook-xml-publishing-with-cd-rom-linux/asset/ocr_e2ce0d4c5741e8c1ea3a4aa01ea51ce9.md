# Understanding DocBook

```
<!DOCTYPE book PUBLIC "//OASIS//DTD DocBook V4.1//EN"
intro.sgml>

<!ENTITY appendix SYSTEM "Appendix.sgml">

intro:
  &include;
  &appendix;
n
"test.sgml" [New] 13L. 241C written
```

Figure 1.2 Calling multiple files from the document declaration

An element describes a document, either a part of its structure or some of the text inside it. Elements are referred to as tags when they're used in marking up a document. Again, if you're familiar with HTML, you will be comfortable with the concept of elements.

The content inside a set of tags sometimes needs more description than an element of markup by itself provides, so many elements also have attributes, which further describe the content within the markup.

Elements and their potential attributes are described in the DTD. You can't make up elements or their attributes on the fly; they must be described in the DTD to be valid.

> Technically speaking, you can make up elements on the fly in XML documents, but not if they're using the DocBook DTD. XML is designed to allow authors to create well-formed documents that need no DTD. However, for the purposes of DocBook, you will always want to stick to the elements described in the DTD. Why? Because DocBook is designed to be portable and to allow others to share information. If you stray from the DTD, you will negate the benefits of working with DocBook in the first place.

The content of attributes, however, is often open. One example would be the <sect1> element. It's perfectly valid to use the <sect1> element by itself, and

![](bbox=[0.835, 0.705, 0.935, 0.905])