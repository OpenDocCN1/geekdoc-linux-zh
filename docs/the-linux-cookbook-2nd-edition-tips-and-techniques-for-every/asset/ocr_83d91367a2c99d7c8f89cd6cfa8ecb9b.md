Sometimes, simple outputting of text is quite appropriate, such as when you just want to display one line of a file, or when you want to display the first or last part of a file.

This section describes the tools used for such purposes. These tools are best used as filters, often at the end of a pipeline, taking their input from the output of other commands. To display text in a font, first convert it to PostScript and view that (see Recipe 15.2 [Outputting Text to PostScript], page 359).

# 9.2.1 Displaying Non-Printing Characters

Use cat with the -v option to output non-printing characters, such as control characters, in such a way that you can see them. With this option, cat outputs those characters in hat notation, where they are represented by a caret (^) and the letter or other character corresponding to the actual control character (for example, a “Control-G” or bell character would be output as “^G”).

⇒ To output the file translation with all non-printing characters displayed in hat notation, type:

```
$ cat -v translation [RET]
```

To visually display the end of each line, use the -E option; it specifies that a “$” should be output after the end of each line. This is useful for determining whether lines contain trailing space characters. (You can also use grep to output lines containing trailing spaces.)

Also useful is the -T option, which outputs tab characters as their literal control character, written in hat notation as “^I.”

The -A option combines all three of these options—it is the same as specifying -vET.

⇒ Here are some ways to use this.

+   - To output the file translation with a “$” character displayed at the end of every line, type:
+     $ cat -E translation [RET]

+   - To output the file translation with all tab characters written as “^I” instead of literal tabs, type:
+     $ cat -T translation [RET]

+   - To output the file translation with non-printing characters, including tabs, displayed in hat notation, and with a “$” character displayed at the end of each line, type:
+     $ cat -A translation [RET]