# Advanced Bash–Scripting Guide

If the file contains tabs or nonprintable characters, this may cause unpredictable behavior. In such cases, considering expand and unexpand in a pipe preceding colrm.

nl filtering. nl filename lists filename to stdout, but inserts consecutive numbers at the beginning of each non-blank line. If omitted, operates on stdin.

The output of nl is very similar to cat -n, however by default nl does not list blank lines.

# 12–21. nl: A self-numbering script.

```
#!/bin/bash
# This script echoes itself to stdout with its lines numbered
# 'nl' sees as line 3 since it does not number blank lines.
# 'cat -n' sees the above line as number 5
nl 'basename $0'
echo; echo # Now, let's try it with 'cat -n'
cat -n $basename $0
# The difference is that 'cat -n' numbers the blank lines.
# Note that 'nl -ba' will also do so.
exit 0
```

Print formatting. This will paginate files (or stdout) into sections for hard copy printing or viewing on screen. Various options permit row and column manipulation, joining lines, settings, numbering lines, adding page headers, and merging files, other things. The pr command combines much of the functionality of nl, paste, fold, column, and expand.

```
pr -o 5 --widths=65 fileZZ | gives a nice paginated to screen of fileZZ margins set at 5 and 65.
```

A particularly useful option is -d, forcing double-spacing (same effect as sed -G).

A GNU utility for localization and translating the text output of programs into foreign languages. primarily intended for C programs, gotten also finds use in shell scripts. See the info page.

A utility for converting file(s) to a different encoding (character set). Its chief use is for localization.

# 12.4. Text Processing Commands