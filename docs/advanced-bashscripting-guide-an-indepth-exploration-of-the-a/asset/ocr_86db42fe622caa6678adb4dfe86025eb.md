# Advanced Bash–Scripting Guide

```
b=`ls /usr/local/bin`      # Get a file listing...
echo $b | fmt -w $WIDTH

# Could also have been done by
# echo $b | fold -w $WIDTH

exit 0
```

See [Example 12–4].

A powerful alternative to **fmt** is Kamil Tolan's **par** utility, available from http://cs.berkeley.edu/~ame/Par/

The **ptx [targetfile]** command outputs a permuted index (cross-reference list) of the targetfile. This may be further filtered and formatted in a pipe, if necessary.

This deceptively named filter removes lines from an input stream. It also attempts to replace whitespace with equivalent tabs. The chief of **col** is in filtering the output from certain text processing utilities, such as **groff** and **tbl**.

Column formatter. This filter transforms list-type text output into a "pretty-printed" table by inserting tabs at appropriate places.

# Example 12–20. Using column to format a directory listing

```
#!/bin/bash
# This is a slight modification of the example file in the "column" man page.

(printf "%PERMISSIONS OWNER GROUP SIZE MONTH DAY HH:MM PROG-NAME\n" \
; ls -l | sed 1 | column -t)

# The "sed 1d" in the pipe deletes the first line of output,
#+ which would be "total"
# where "N" is the total number of files found by "ls -l".

# The -t option to "column" pretty-prints a table.

exit 0
```

Column remover. This removes columns (characters) from a file and writes the file, lacking the range of specified columns, back to **stdout**. **colrm 2 4 <filename>** removes the second through fourth characters from each line of the text **filename**.

# 12.4. Text Processing Commands