True; print the full file name on the standard output, followed by a newline. If you are piping the output of **find** into another program and there is the faintest possibility that the files which you are searching for might contain a newline, then you should seriously consider using the **-print0** option instead of **-print**. See the **UNUSUAL FILENAMES** section for information about how unusual characters in filenames are handled.

-print0

True; print the full file name on the standard output, followed by a null character (instead of the newline character that **-print** uses). This allows file names that contain newlines or other types of white space to be correctly interpreted by programs that process the **find** output. This option corresponds to the **-0** option of **xargs**.

-printf *format*

True; print *format* on the standard output, interpreting '`\`' escapes and '`%'` directives. Field widths and precisions can be specified as with the '`printf`' C function. Please note that many of the fields are printed as %s rather than %d, and this may mean that flags don't work as you might expect. This also means that the '`-`' flag does work (it forces fields to be left-aligned). Unlike **-print**, **-printf** does not add a newline at the end of the string. The escapes and directives are:

+      \a
+           Alarm bell.

+      \b
+           Backspace.

+      \c
+           Stop printing from this format immediately and flush the output.

+      \f
+           Form feed.

+      \n
+           Newline.

+      \r
+           Carriage return.

+      \t
+           Horizontal tab.

+      \v
+           Vertical tab.

+      \0
+           ASCII NUL.

+      \\
+           A literal backslash (`\`).

+      \NNN
+           The character whose ASCII code is NNN (octal).

A '`\`' character followed by any other character is treated as an ordinary character, so they both are printed.