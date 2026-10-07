begins on and then writing a table of contents that will change if many revisions are made. Nope, it's generated-on-the-fly each time you process the document to create output.

However, I'll include a brief example of a table of contents so that you can see the work you're avoiding. The elements used to create this table of contents are Toc, TocPart, Tocchap, and Toentry. Although this is helpful to understand, I've always found the table of contents generated-on-the-fly to be good enough, as long as you include the Title element for each Sect and Chapter and similar elements.

```
<toc>
<tocpart>
<tocchap>
<tocentry pagenum="1">How to make a TOC</tocentry>
<tocentry pagenum="2">How to avoid making a TOC</tocentry>
</tocchap>
</tocpart>
</toc>
```

# # Creating a Glossary

If you use many unfamiliar terms or jargon in your book, you should include a glossary to which readers can refer. Any technical reference worth its salt (and many other types of books) includes a glossary. The Glossary element can be contained within a Chapter element (or any of the Sect1 through Sect5 elements), the Book element, and if you have several entries for a glossary, you might want to set it off in its own file, similar to the examples for the Chapter elements in this chapter.

Glossaries with more than a few entries should probably make use of the Gloss element, which allows the glossary to be divided into manageable divisions. Generally, I would recommend divying up your glossary alphabetically, unless there is a more logical way to divide it.

The following example shows a DocBook glossary with two logical divisions and a few sample entries. Of course, a real glossary would be much heft than this, but this should be sufficient to give you an idea of what the markup looks like for the Glossary element and its children. Figure 4.12 shows the glossary rendered in HTML.

```
<!DOCTYPE glossary PUBLIC "//OASIS//DTD DocBook V4.1//EN">
<glossary>
```