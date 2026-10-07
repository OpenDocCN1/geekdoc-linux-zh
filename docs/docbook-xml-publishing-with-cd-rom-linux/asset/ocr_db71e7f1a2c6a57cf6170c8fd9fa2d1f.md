# Chapter 5: Making Online Documents

Figure 5.1 shows what the ULink looks like after being rendered into HTML using the default stylesheets. However, the information is not lost in print publications. Figure 5.2 shows the DocBook markup output to PostScript.

Obviously, you can't click on a link in a paper document and go to a Web site. However, the URL for the site is neatly printed next to the title of the site so it can be manually entered if the reader wishes.

The ULink element can also be used for linking to files on an FTP server to an Archie or Gopher server—it could also be used for protocols that don't exist yet.

To give another example, maybe your document link should link to an FTP server to retrieve extra documentation (see Figure 5.3). The syntax is such as:

```
<para>
You can find supplemental documentation at this FTP site:
<ulink url="http://yourserver.net/documents/extra.sgml">
<title>http://yourserver.net/documents/extra.sgml</title>
</ulink>
</para>
```

![](bbox=[0.163, 0.566, 0.866, 0.946])

# Chapter 1. ULink Element

The offset is/DocBook Website
This is an example of an ULink element in DocBook.

Figure 5.1 A link from DocBook in HTML