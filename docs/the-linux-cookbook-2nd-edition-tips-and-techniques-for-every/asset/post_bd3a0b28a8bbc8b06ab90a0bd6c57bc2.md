
⇒ Here are two ways to use this.

- To peruse the file index.html with its HTML tags removed, type:

  ```
  $ unhtml index.html | less [RET]
  ```

- To remove the HTML tags from the file index.html and write the output to a file called index.txt, type:

  ```
  $ unhtml index.html > index.txt [RET]
  ```

**NOTES:** When you remove the HTML tags from a file with unhtml, no further formatting is done to the text. Furthermore, it only works on files, and not on URLs themselves.

### METHOD #2

| Package | DEB | RPM | WWW |
| --- | --- | --- | --- |
| Lynx | lynx | lynx | http://lynx.browser.org/ |

Use lynx to save an HTML file or a URL as a formatted text file, so that the resultant text looks like the original HTML when viewed in lynx. It can also preserve italics and hyperlink information in the original HTML. See Recipe 33.2.4 [Sending Text from the Web to Standard Output], page 646.

One thing you can do with this lynx output is pipe it to tools for spacing text, and then send that to enscript for setting in a font. This is useful for printing a Web page in typescript “manuscript” form, with images and graphics removed and text set double-spaced in a Courier font.

⇒ To print a copy of the URL http://example.com/essay/ in typescript manuscript form, type (all on one line):

```
$ lynx -dump -underscore -nolist http://example.com/essay/ | pr -d | enscript -B [RET]
```

**NOTES:** In some cases, you might want to edit the file before you print it, such as when a Web page contains text navigation bars or other text that you’d want to remove before you turn it into a manuscript. In such a case, you’d pipe the lynx output to a file, edit the file, and then use pr on the file and pipe that output to enscript for printing.

### METHOD #3

| Package | DEB | RPM | WWW |
| --- | --- | --- | --- |
| Html2ps | html2ps | html2ps | http://www.tdb.uu.se/~jan/html2ps.html |

Use html2ps to convert an HTML file to PostScript; this is useful when you want to print a Web page with all its graphics and images, or when you want to convert all or part of a Web site into PDF. Give the URLs or file names of the HTML files to convert as options. Use the -u option to underline the anchor text of hypertext links; specify a file name to write to as an argument to the -o option. The defaults are to not underline links and to write to the standard output.

⇒ Here are two ways to use this.

- To print a PostScript copy of the document at the URL http://example.com/essay/ to the default printer, type:

  ```
  $ html2ps http://example.com/essay/ | lpr [RET]
  ```

- To write a copy of the document at the URL http://example.com/essay/ to a PostScript file submission.ps with all hypertext links underlined, type:

  ```
  $ html2ps -u -o submission.ps http://example.com/essay/ [RET]
  ```

## 33.9.3 Validating HTML

| Package | DEB | RPM | WWW |
| --- | --- | --- | --- |
| Weblint | weblint | weblint | http://www.webmaster.bham.ac.uk/weblint/ |

Use weblint to validate the basic structure and syntax of an HTML file. Give the name of the file to be checked as an argument, and weblint outputs any complaints it has about the file to standard output, such as whether or not IMG elements are missing ALT descriptions, or whether nested elements overlap.

⇒ To validate the HTML in the file index.html, type:

```
$ weblint index.html [RET]
```

## 33.10 Analyzing Your Web Traffic

If you have a Web site, you will undoubtedly have some interest in analyzing your Web traffic: knowing which pages are popular, who is looking at them, when they are looking and where they are coming from. Do this by retrieving the Web logs from the server that hosts your site—these are plain text files written by the server containing data for every access of your site, one per line. Tools exist to analyze these logs; here are the two easiest methods for doing this.

### METHOD #1

| Package | DEB | RPM | WWW |
| --- | --- | --- | --- |
| Analog | analog | analog | http://www.analog.cx/ |

The most popular tool in use for analyzing Web logs is analog, which produces a comprehensive set of reports, including the following:

- The top words people used in search engines to find your site.
- The *referrers*, which are pages with links that the requesting computers followed to get to your pages.
- The top organizations of the computers that requested your pages.
- The operating systems of the computers that requested your pages.
- The most popular directories on your site.
- The most popular files on your site.

Give the filespec for the log files to analyze as an argument to analog. This command reads the log file you give and it outputs the reports to the standard output. Output is in HTML format; either pipe it to the standard input of a Web browser to view it or redirect it to a file to save it. Log files have to be in a log format that analog can recognize, such as the format used by the popular Apache Web server; they can also be compressed.

⇒ Here are some ways to use this.

- To view an analysis of `~/web/logs/2005/www.20050408.gz`, a Web log file, type:

  ```
  $ analog ~/web/logs/2005/www.20050408.gz | lynx -stdin
  ```
