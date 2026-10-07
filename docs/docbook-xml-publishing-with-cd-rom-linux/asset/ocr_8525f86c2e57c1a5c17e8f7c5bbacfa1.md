# Notes, Cautions, Tips, and Warnings 239

There is also an InformalExample element, if you want to have an example without a title. For general output, there's not much of a reason to use the InformalExample element in combination with the ProgramListing element.

# Notes, Cautions, Tips, and Warnings

If you read a lot of computer books like I do, you've probably noticed that there is an abundance of tips, notes, and warnings. These are set off from the text with an icon to alert you to particularly evil things that can happen if you do the wrong thing, or clue you in special commands or tricks that you can use. DocBook has five elements that can be used to highlight sections of the documentation—Caution, Important, Note, Tip or Warning. The element names are pretty descriptive of their function, and they're all used in the same fashion. The next code sample shows the Tip element in use, but the general syntax is for any of these elements.

```
<!DOCTYPE article PUBLIC "//OASIS//DTD DocBook V4.1//EN">
<article><title>Example</title>
<para>This is a regular paragraph.</para>
<tip><title>A Helpful Tip</title>
<para>This paragraph contains the text of the Tip element.</para>
<para>The Tip element may contain several paragraphs and even screenshots, figures, lists and other types of content.</para>
</tip>
</article>
```

Each of the five elements may have a Title element, but it is not required. When rendered in HTML, PostScript, or several other formats, these elements will also have an icon or graphic that draws the reader's attention to the item. Figure 12.4 shows the tip from the code output as HTML.

When you render a document in plain text using SGMLTools the obviously you won't be able to include a great deal of special formatting. However, the text will be set off slightly from regular text to separate the tip from the rest of the content, as shown in Figure 12.5.

Visual clues like these stick in our minds more clearly than the majority of the text, so it might be helpful to your readers if you try to make a point of using these elements when appropriate. Sometimes a really good tip or a warning that keeps you from sending your data to the big bit bucket in the sky is worth reading an entire article for. Using these elements appropriately sparingly, can be a big help to your readers.