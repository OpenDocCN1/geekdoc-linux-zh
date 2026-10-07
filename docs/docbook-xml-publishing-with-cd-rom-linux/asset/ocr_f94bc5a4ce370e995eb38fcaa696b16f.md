# Creating Online Documentation

# How XRef Works

XRef pulls the information needed from the ID attribute and the Title element, or if the element does not contain a child element, it uses the XRefLabel attribute. If an element does not support the Title child element or the XRefLabel attribute, you must use the Anchor element, which can be located virtually anywhere within a document, as long as it is nested within one of its parent elements.

Your head swimming from confusing jargon? Are child and parent elements and attributes confusing you? If you skipped the Introduction, now might be a good time to backtrack and skim through it. You can also check out Appendix A, "DocBook Glossary," if you are just a little fuzzy on the terms.

If you feel confused, don't think you're alone: DocBook wasn't created with user-friendliness in. The concepts behind DocBook aren't impossible to get a handle on, but it might help to take a breather occasionally and absorb what you've covered.

DocBook markup is literally another language, admittedly a limited one based on English but still a foreign tongue. Everyone knows that it takes patience and time to pick up a foreign language; the same goes for DocBook. The downside to DocBook, compared with real languages, is that there's nowhere you can go to immerse yourself in the spoken language, and there's no native cuisine for DocBook either—unless you count native geek foods such as pizza, Chinese takeout, and any caffeinated beverage.

![](bbox=[0.823, 0.573, 0.947, 0.693])

NOTE

To use XRef to link to a section within your document, you do something like the following:

```
<sect1 id="xref">
  <title>Using XRef</title>

</sect1>
<xref linkend="xref">
```