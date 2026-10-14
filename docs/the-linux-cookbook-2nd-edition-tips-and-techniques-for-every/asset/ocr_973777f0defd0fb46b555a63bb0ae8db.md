NOTES: This regexp will still output lines that contain only tab characters.

# METHOD #3

To remove from the output all empty lines, and lines that contain only a combination of tab or space characters, use grep with "^[[:space:]]." as the regexp to search for. It uses the special predefined "[:space:]" regexp class, which matches any kind of space character at all, including tabs.

⇒ To output only the lines from the file term-paper that contain more than just space or tab characters, type:

```
$ grep '^[[:space:]].' term-paper RET
```

# METHOD #4

If a file is double-spaced, where all even lines are blank, you can remove those lines from the output by using sed with the "n;d" expression.

⇒ To output only the odd lines from file term-paper, type:

```
$ sed 'n;d' term-paper RET
```

# 13.1.3 Double-Spacing Text

To double-space text, where one blank line is inserted between each line in the original text, use the pr tool with the -d option. By default, pr paginates text and puts a header at the top of each page with the current date, time, and page number; use the -t option to omit this header.

⇒ Here are two ways to use this.

+   - To double-space the file term-paper and write the output to the file term-paper.print, type:
+     $ pr -d -t term-paper > term-paper.print RET

+   - To double-space the file term-paper and send the output directly to the printer for printing, type:
+     $ pr -d -t term-paper | lpr RET

NOTES: The pr ("print") tool is a text pre-formatter, often used to paginate and otherwise prepare text files for printing; more discussion on the use of this tool is in Recipe 13.3 [Paginating Text], page 312.

# 13.1.4 Triple-Spacing Text

To triple-space text, where two blank lines are inserted between each line of the original text, use sed with the "G;G" expression.