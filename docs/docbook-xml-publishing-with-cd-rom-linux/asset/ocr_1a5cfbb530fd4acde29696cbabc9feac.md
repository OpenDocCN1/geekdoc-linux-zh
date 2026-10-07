# Chapter 4: Preparing a Book with DocBook

of appendixes in a DocBook book. As the following example shows, the Appendix element is used in the same way as the Chapter element. The only valid parent elements for an appendix are the Article, Book, and Part elements. An appendix may not be included in a chapter, for example.

```
<!DOCTYPE appendix PUBLIC "-//OAS//DTD DocBook V4.1//EN">
<appendix>
<title>This is an Appendix.</title>
<para>Not too difficult, is itit</para>
</appendix>
```

Not much to that at all, there is. As of DocBook version 4.x, the Appendix element may also contain an AppendixInfo element if you want to include meta information about the appendix. Also, just as with the Chapter element, you can include a number of other elements within an appendix, including a Sidebar, a Table, an Itemizedlist, and many others. See Appendix B for the full list of potential child elements.

![](bbox=[0.05, 0.465, 0.175, 0.635])

> You should familiarize yourself with the appropriate child elements for each other element. Sometimes it jogs your memory to include further information about something you have forgotten. For instance, the Sidebar element is valid within the Appendix element, which might remind you to include a sidebar about something in the appendix you have forgotten or have structured differently.

# Creating a Bibliography

The last major element I'm going to talk about in this chapter is the Bibliography element. A bibliography, if you're not familiar with one, includes information about books used for reference in writing an article or book or perhaps books that are suggested reading.

If you've ever written college term papers, you're probably painfully familiar with bibliographies. The nice thing about the Bibliography element and its children is that if yourประเทศไทย is set up to output in the proper formats, it is much easier to generate a bibliography in MLA or APA formats than in a traditional word processor. All you have to do is fill in the proper elements, and the processing program should do the rest. I'll talk more about stylesheets in Chapter 10, "Customizing DocBook"