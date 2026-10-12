+   6. To view the HTML file just created, I typed the following:

```
$ epiphany $HOME/doc-test/cardoc/t2.html
```

Figure 6-11 shows an example of the output created from the db2html1 command. The screen on the left shows the first page. Click on the Next link at the top of the page. The second page that you see is shown on the right. During conversion to HTML, the db2html1 command adds Next/Previous buttons to each page. It also puts the title of each section in a Table of Contents on page one and in the browser's title bar.

![](bbox=[0.06, 0.26, 0.74, 0.57])

**Figure 6-11:** The DocBook file is output in HTML with the db2html command.

From this point, you can continue to add content and different types of tags. If you are writing documents for a particular project (such as the Linux projects mentioned earlier), you should get information on the particular tags and other style issues they require.

# ### Converting DocBook documents

The previous example shows how to create a simple DocBook document and convert it to HTML output. The following Red Hat Linux utilities convert DocBook to other formats:

+   - **docbook2dv** — Converts a DocBook file to Device Independent file format.

+   - **docbook2html** — Converts a DocBook file to HTML format.

+   - **docbook2man** — Converts a DocBook file to man page format.

+   - **docbook2pdf** — Converts a DocBook file to Portable Document Format (PDF).

+   - **docbook2ps** — Converts a DocBook file to PostScript format.

+   - **docbook2rtf** — Converts a DocBook file to Rich Text Format (RTF).