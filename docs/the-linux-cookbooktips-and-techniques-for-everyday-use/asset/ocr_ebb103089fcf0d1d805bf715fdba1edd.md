**NOTE:** You can also use `cat` to concatenate files that are *not* text, but its most popular usage is with text files. Another way to concatenate files of text in an automated way is to use file inclusion——see [Including Text Files](.).

A similar tool, `zcat`, reads the contents of compressed files.

+   11.6.1 Writing Text to Files
+   Writing text to a file.
+   11.6.2 Appending Text to a File
+   Appending text to the end of a file.
+   11.6.3 Inserting Text at the Beginning of a File
+   Inserting text to the beginning of a file.

# 11.6.1 Writing Text to Files

Sometimes, it's too much trouble to call up a text editor for a particular job—you just want to write a text file with two lines in it, say, or you just want to append a text file with one line. There are ways of doing these kind of micro-editing jobs without a text editor.

To write a text file without using a text editor, redirect the standard output of `cat` to the file to write. You can then type your text, typing **C-d** on a line of its own to end the file. This is useful when you want to quickly create a small text file, but that is about it; usually, you open or create a text file in a text editor, as described in the previous sections in this chapter.

+   • To make a file, `novels`, with some text in it, type:

```
$ cat 62; novels RET
This Side of Paradise RET
The Beautiful and Damned RET
The Great Gatsby RET
Tender Is the Night RET
C-d
$
```

In this example, the text file `novels` was created and contains four lines of text (the last line with the **C-d** is never part of the file).

Typing text like this without an editor will sometimes do in a pinch but, if you make a mistake, there is not much recourse besides starting over—you can type **C-u** to erase the current line, and **C-c** to abort the whole thing and not write the text to a file at all, but that's about it.