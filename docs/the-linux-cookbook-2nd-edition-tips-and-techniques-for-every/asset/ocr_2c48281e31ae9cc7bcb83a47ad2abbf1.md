⇒ To view the HTML-formatted text file homepage.html as HTML source code, type:

```
$ less homepage.html [RET]
```

# METHOD #2

To view an HTML-formatted text file with the HTML formatting applied to the text, open the file in a Web browser as described in Methods #2 and #3 of Recipe 5.10 [Browsing Files and Directories], page 157.

⇒ To view the HTML-formatted text file homepage.html as rendered HTML, type:

```
$ mozilla homepage.html [RET]
```

# 9.3.2 Viewing NROFF-Formated Text

To view text written in NROFF format, which is intended for use with the TROFF or GROFF text processors, use man with the -l option. Give the name of the file to view as an argument (use "-" as the file argument to view the standard input). By default, man sends its output to less so you can peruse it.

⇒ Here are two ways to use this.

+   - To view the NROFF file program.1, type:
+     $ man -l program.1 [RET]

+   - To convert the NROFF file program.1 to text, and write that text to a new file program.txt, type:
+     $ man -l program.1 > program.txt [RET]

In this last example, the new file program.txt will contain overstrike characters for boldface text. The original file program.1 is unaltered.

NOTES: All man pages are written in NROFF format, hence the use of that command to view it.

# 9.3.3 Viewing C Program Source Code

There are at least two methods for viewing C program source code.