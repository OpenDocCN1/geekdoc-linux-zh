There are three major variants of grep, controlled by the following options:

+   -   **-G**, **--basic-regexp** Interpret *pattern* as a basic regular expression (see below). This is the default.
+       -   **-E**, **--extended-regexp** Interpret *pattern* as an extended regular expression (see below).
+       -   **-F**, **--fixed-strings** Interpret *pattern* as a list of fixed strings, separated by newlines, any of which is to be matched.

In addition, two variant programs **egrep** and **fgrep** are available. **egrep** is similar (but not identical) to **grep** **-E**, and is compatible with the historical Unix **egrep**. **fgrep** is the same as **grep** **-F**.

All variants of grep understand the following options:

+   -   **-num** Matches will be printed with *num* lines of leading and trailing context. However, **grep** will never print any given line more than once.
+       -   **-A** *num*, **--after-context**=*NUM* Print *num* lines of trailing context after matching lines.
+       -   **-B** *num*, **--before-context**=*NUM* Print *num* lines of leading context before matching lines.
+       -   **-C**, **--context** Equivalent to **-2**.
+       -   **-V**, **--version** Print the version number of **grep** to standard error. This version number should be included in all bug reports (see below).
+       -   **-b**, **--byte-offset** Print the byte offset within the input file before each line of output.
+       -   **-c**, **--count** Suppress normal output; instead print a count of matching lines for each input file. With the **-v**, **--invert-match** option (see below), count non-matching lines.
+       -   **-e** *pattern*, **--regexp**=*PATTERN* Use *pattern* as the pattern; useful to protect patterns beginning with -.
+       -   **-f** *file*, **--file**=*FILE* Obtain the pattern from *file*.
+       -   **-h**, **--no-filename** Suppress the prefixing of filenames on output when multiple files are searched.