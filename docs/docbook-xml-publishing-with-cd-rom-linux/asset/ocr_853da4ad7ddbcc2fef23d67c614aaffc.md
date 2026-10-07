# Chapter 6: Parsing DocBook

apparent. Even if you don't use DocBook to create any other type of output, the benefits from creating HTML alone are worth it. When you output PostScript or other formats, you maximize the benefits.

# Text

Where we would be without plain-text files? This is the one format you can count on to be compatible with just about any platform.

To generate plain text from your DocBook document, you use the back-end as shown in Figure 6.9.

```
sgmltools -b tbt book.sgml
```

SGMLtools creates one ASCII text file from your document. This should be viewable on nearly any platform.

# RTF

If you want to create a file for use with Microsoft Word, you use the Rich Text Format backed. Although this isn't a Word document, per se, it is compatible

![](bbox=[0.195, 0.535, 0.93, 0.865])

Figure 6.9 The same file output to parse plain text