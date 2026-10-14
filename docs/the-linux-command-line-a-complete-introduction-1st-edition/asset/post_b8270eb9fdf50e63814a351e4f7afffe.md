
+   3) comped
+   4) limped
+   5) pimped
+   1) Ignore
+   r) Replace
+   a) Add
+   b) Abort
+   8) humped
+   9) impede
+   0) umped
+   I) Ignore all
+   R) Replace all
+   1) Add Lower
+   x) Exit

?

At the top of the display, we see our text with a suspiciously spelled word highlighted. In the middle, we see 10 spelling suggestions numbered 0 through 9, followed by a list of other possible actions. Finally, at the very bottom, we see a prompt ready to accept our choice.

If we enter 1, aspell replaces the offending word with the word jumped and moves on to the next misspelled word, which is lazy. If we select the replacement lazy, aspell replaces it and terminates. Once aspell has finished, we can examine our file and see that the misspellings have been corrected:

```
[me@linuxbox ~]$ cat foo.txt
The quick brown fox jumped over the lazy dog.
```

Unless told otherwise via the command-line option --dont-backup, aspell creates a backup file containing the original text by appending the extension .bak to the filename.

Showing off our sed editing prowess, we’ll put our spelling mistakes back in so we can reuse our file:

```
[me@linuxbox ~]$ sed -i 's/lazy/laxy/; s/jumped/jimped/' foo.txt
```

The sed option -i tells sed to edit the file "in place," meaning that rather than sending the edited output to standard output, it will rewrite the file with the changes applied. We also see the ability to place more than one editing command on the line by separating them with a semicolon.

Next, we’ll look at how aspell can handle different kinds of text files. Using a text editor such as vi (the adventurous may want to try sed), we will add some HTML markup to our file:

```
<html>
  <head>
    <title>Mispelled HTML file</title>
  </head>
  <body>
    <p>The quick brown fox jimped over the laxy dog.</p>
  </body>
</html>
```

Now, if we try to spellcheck our modified file, we run into a problem. If we do it this way:

```
[me@linuxbox ~]$ aspell check foo.txt
```

we'll get this:

```
<html>  <head>
    <title>Misspelled HTML file</title>
  </head>
  <body>
    <p>The quick brown fox jmped over the lazy dog.</p>
  </body>
</html>
```

+   1) HTML
+   2) ht ml
+   3) ht-ml
+   4) Ignore
+   r) Replace
+   a) Add
+   b) Abort
+   4) Hamel
+   5) Hamil
+   6) hotel
+   I) Ignore all
+   R) Replace all
+   l) Add Lower
+   x) Exit

?

aspell will see the contents of the HTML tags as misspelled. This problem can be overcome by including the -H (HTML) checking-mode option, like this:

```
[me@linuxbox ~]$ aspell -H check foo.txt
```

Our result is this:

```
<html>  <head>
    <title>Misspelled HTML file</title>
  </head>
  <body>
    <p>The quick brown fox jmped over the lazy dog.</p>
  </body>
</html>
```

+   1) Mi spelled
+   2) Mi-spelled
+   3) Misspelled
+   4) Dispelled
+   5) Spelled
+   6) Ignore
+   r) Replace
+   a) Add
+   b) Abort
+   6) Misapplied
+   7) Miscallied
+   8) Respelled
+   9) Misspell
+   0) Misled
+   I) Ignore all
+   R) Replace all
+   l) Add Lower
+   x) Exit

?

The HTML is ignored, and only the non-markup portions of the file are checked. In this mode, the contents of HTML tags are ignored and not checked for spelling. However, the contents of ALT tags, which benefit from checking, are checked in this mode.

Note: By default, aspell will ignore URLs and email addresses in text. This behavior can be overridden with command-line options. It is also possible to specify which markup tags are checked and skipped. See the aspell man page for details.

## Final Note

In this chapter, we have looked at a few of the many command-line tools that operate on text. In the next chapter, we will look at several more. Admittedly, it may not seem immediately obvious how or why you might use some of these tools on a day-to-day basis, though we have tried to show some semi-practical examples of their use. We will find in later chapters that these tools form the basis of a tool set that is used to solve a host of practical problems. This will be particularly true when we get into shell scripting, where these tools will really show their worth.

## Extra Credit

There are a few more interesting text-manipulation commands worth investigating. Among these are split (split files into pieces), csplit (split files into pieces based on context), and sdiff (side-by-side merge of file differences).
