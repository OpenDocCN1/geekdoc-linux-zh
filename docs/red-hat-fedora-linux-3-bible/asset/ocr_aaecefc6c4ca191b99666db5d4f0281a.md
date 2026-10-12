The first thing you will learn is how to figure out what you can afford.
`</para>`
`</section>`
`<section>`
`<title>The Next Step</title>`
`<para>`
After you know what you can afford, you can begin your search.
`</para>`
`</section>`
`</article>`

There are a few things you should notice about this document. The entire document is wrapped in article tags (`<article>` `</article>`). The article title is in title tags (`<title>` `</title>`). The section tags (`<section>` `</section>`) indicate sections of text that have a title and paragraph each. These sections can later be treated separately in the TOC.

+   4. Save the file and exit from the text editor.
+   5. Next, you can try translating the document you just created into several different formats. For example, to create HTML output you could type the following:
+   `$ db2html1 cardoc.sgm`
+   
+   The result is a new directory called cardoc. The result from db2html1 in the cardoc directory was: stylesheet-images directory, t2.html file, and x12.html file.
+   6. To view the HTML file just created, I typed the following:
+   `$ ephany $HOME/doctest/cardoc/t2.html`

Figure 6-11 shows an example of the output created from the db2html1 command. The screen on the left shows the first page. Click the Next link at the top of the page. The second page that you see is shown on the right. During conversion to HTML, the db2html1 command adds Next/Previous buttons to each page. It also puts the title of each section in a Table of Contents on page one and in the browser's title bar.

From this point, you can continue to add content and different types of tags. If you are writing documents for a particular project (such as the Linux projects mentioned earlier), you should get information on the particular tags and other style issues they require.