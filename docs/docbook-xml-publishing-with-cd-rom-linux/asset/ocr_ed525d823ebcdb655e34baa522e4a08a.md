# Rendering Web pages with SGMLTools-Lite

To create Web pages from your DocBook documents, you use the HTML back end. Note that the HTML output, although valid, is ugly. In Chapter 5, “Creating Online Documents,” are examples of using Tidy to clean up Doc-Book output and convert some of the physical formatting tags to cascading stylesheets.

To render HTML, use the following command:

```
sgmltools -b html book.sgml
```

This creates a directory named book/ with the HTML file or files in it. The number of files output depends on the sections you have in your document. Figure 6.8 HTML output from using SGMLtools.

Again, you have an index and navigation generated on-the-fly without having to go through the drudgery of doing it by hand. When you create a document only once and never modify it, you don't see the benefits as much, but if you work with a document for a while (a living document, that is), the benefits of using DocBook rather than hand-coding HTML become very

![](bbox=[0.052, 0.532, 0.725, 0.935])

Figure 6.8 HTML output from DocBook