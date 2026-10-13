from matching the phone numbers. These characters are commonly called anchors because they anchor a pattern to the start or end of a line. Because 1998 and 1999 are both at the beginning of a line, this will be easy.

If ^ is used outside of a range, the ^ character matches the start of a line.

$ matches the end of a line. If your pattern falls at the end of a line, you can anchor it in this position with $.

For example, type the following:

```
>grep "^[7-8][0-9]*" sample.txt
```

1998
1999

That's more like it. Only the two dates are returned, because they fall at the beginning of a line. The phone numbers no longer match because the portion that did match is not at the start of the line.

# USES FOR REGULAR EXPRESSIONS

What you've just learned is only a very tiny subset of the regular expressions that you can generate. Regular expressions can be used in a wide variety of different applications. For example, sed, the stream editor, can replace patterns of text from a stream of text on the fly. (It's great for editing a STDOUT -> STDIN stream between two programs!) Being able to do a global regular expression search and replace on a thousand files—rather than editing each individually—is a thing of beauty. When you are using the shell you can also use a subset of the complete regular expression library to specify filenames for operations.

For example, if you have a group of files named test1, test2, test3, test4, and test5, and you want to copy files 3 through 5 to a new directory, you can use a regular expression such as the following:

```
>cp test[3-5] newdirectory
```

You'll need to consult the man pages for the shell you are running in order to determine which regular expressions it supports. The same goes for everything else that uses regular expressions. Unfortunately, even though REs themselves are pretty standard, the extent to which any individual application supports them is entirely up to that application. Perl, for example, is an application (and, in turn, is a complete programming environment) which makes extensive use of regular expressions.