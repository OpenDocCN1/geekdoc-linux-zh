+   - [q] to quit
+   - [Enter] to page down line by line
+   - [Space] to page down page by page
+   - [b] to page back up by one page
+   - [/] followed by a string and [Enter] to search for a string
+   - [n] to find the next occurrence of the previous search

There are times when it’s just a lot more convenient to read something from a sheet of paper. Providing you have a working printer, you can print man pages as well. If you don’t have PostScript printing capability and just want to print ASCII, you can print man pages with:

```
man COMMAND | lpr
```

If you do have a PostScript printer, you will probably want to print with:

```
man -t COMMAND | lpr
```

In both of those commands substitute “COMMAND” for the command you are trying to get help for.

Sometimes you’ll find that certain system components have more than one man page. Here is a table showing the sections that are used to divide man pages: