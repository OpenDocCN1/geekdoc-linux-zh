# Advanced Bash-Scripting Guide

```
unicode_var='♀'
echo -e $unicode_var      # Female symbol
printf "$unicode_var \n"    # Female symbol, with newline

# And for something a bit more elaborate . . .

# We store Unicode symbols in an associative array,
+# then retrieve them by name.
# Run this in a gnome-terminal or a terminal with a large, bold font
+# for better legibility.

declare -A symbol # Associative array.

symbol[script_E]=\u2130
symbol[script_F]=\u2131
symbol[script_J]=\u2110
symbol[script_M]=\u2133
symbol[Rx]=\u211E
symbol[TEL]=\u2121
symbol[FAX]=\u213B
symbol[care_of]=\u2105
symbol[account]=\u2100
symbol[trademark]=\u2122

echo -n "$symbol[script_E]"
echo -n "$symbol[script_F]"
echo -n "$symbol[script_J]"
echo -n "$symbol[script_M]"
echo -n "$symbol[Rx]"
echo -n "$symbol[TEL]"
echo -n "$symbol[FAX]"
echo -n "$symbol[care_of]"
echo -n "$symbol[account]"
echo -n "$symbol[trademark]"
echo
```

+   * The above examples use '$...'' string-expansion construct.
* When the lastpipe shell option is set, the last command in a pipe doesn't run in a subshell.

Example 37-10. Piping input to a read

```
#!/bin/bash
# lastpipe-option.sh

line=''                         # Null value.
echo "$line = "$line"     # $line =

echo

shopt -s lastpipe              # Error on Bash version -lt 4.2.
echo "Exit status of attempting to set \$lastpipe\" option is $?"
  if 1 Bash version -lt 4.2, 0 otherwise.

echo
```

Chapter 37. Bash, versions 2, 3, and 4 561