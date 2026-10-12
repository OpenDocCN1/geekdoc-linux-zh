3. Enter the tags and text that you want to appear in your document. Most DocBook documents are either <book> type (large, multi-chapter documents) or <article> type (single chapter documents). To try out a DocBook document, type the following:

```
<xml version="1.0">
<article>
<title>Choosing a new car</title>
<artheader>
<abstract>
In this article, you will learn how to price,
negotiate for, and purchase an automobile.
</abstract>
</artheader>
<section>
<title>Getting Started</title>
<para>
The first thing you will learn is how to figure out
what you can afford.
</para>
</section>
<section>
<title>The Next Step</title>
<para>
After you know what you can afford, you can begin your
search.
</para>
</section>
</article>
```

There are a few things you should notice about this document. The entire document is wrapped in article tags (<article> </article>). The article title is in title tags (<title> </title>). The section tags (<section> </section>) indicate sections of text that have a title and paragraph each. These sections can later be treated separately in the TOC.

4. Save the file and exit from the text editor.

5. Next, you can try translating the document you just created into several different formats. For example, to create HTML output you could type the following:

```
$ db2html cardoc.sgml
```

The result is a new directory called cardoc. The result from db2html in the cardoc directory was: stylesheet-images directory, t2.html file, and x12.html file.

6. To view the HTML file just created, I typed the following:

```
$ netscape $HOME/dotcest/cardoc/t2.html
```

Figure 6-9 shows an example of the output created from the db2html command. The screen on the left shows the first page. Click on the Next link at the top of the page. The second page that you see is shown on the right. During conversion to HTML, the