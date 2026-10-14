# 13.2.3 Center-Justifying Text

Use fold to center-justify text, giving the column width as an argument to the -w option. You can also use tr to remove any linefeeds in the text, and then pipe the output to fold.

⇒ Here are some ways to use this.

+   - To center-justify the text in the file log using forty columns, and peruse it on the screen, type:
+     $ fold -w40 log | less [RET]

+   - To center-justify the text in the file log using eighty columns, and write it to a new file called log2, type:
+     $ tr -d '\n' < log | fold -w80 > log2 [RET]

NOTES: This method breaks words across lines.

# 13.3 Paginating Text

A page break in a text file is simply a formfeed character ("Control-L," or octal code 014) that you can insert with a text editor at the point in the file where you want one page to end and another to begin. When you send text with a formfeed character to the printer, the current page being printed is ejected and a new page begins—thus, you can paginate a text file by inserting formfeed characters wherever you want a page break to occur.

You can similarly paginate text in a text editor by manually inserting formfeed characters, but there are also tools that do this automatically, inserting formfeeds throughout the text at set increments, optionally processing the file in other ways to give it pages.

The pr filter is one such tool. It's a general-purpose page formatter and print-preparation utility. By default, it paginates for a length of 66 lines per page, putting a header and footer on each page. The header contains a line with the date, file name, and current page, with two blank lines before and after it; the footer consists of three blank lines to separate the pages. Thus, 56 lines of input text are on each page by default, and the other three lines are the header and footer. Any formfeeds in the text will force a page break at that point, in addition to the regular page breaks just described.

⇒ To print the file duchess with the default pr preparation, type:

```
$ pr duchess | lpr [RET]
```

There are many options that you can use to customize the output of text you paginate.