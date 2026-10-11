In this example the third through tenth lines of the filename are searched for *REGEXP*, and if found, *REGEXP* is replaced with *replacement*.

Addressing can also be used to exclude *REGEXP* matches from being replaced. This is done with the ! (exclamation) character. The following example shows how to ignore the third occurrence of the *REGEXP*.

```
$ sed '`13s/REGEXP/replacement'` filename
```

> **Exam Tip** Pay careful attention to the correct use of regular expressions when using *sed*. You should understand the various ways a string can be located.

**Table 4-19**
**Addressing Used with sed**

| Address | Use |
| :--- | :--- |
| *number* | Specifies the line number to match. |
| *number, number* | Specifies the line numbers to match and includes all lines located between these numbers. |
| $ | Specifies to match the last line. |
| ! | Matches all lines except for the lines specified. |

# ## Using grep

The *grep* utility is used to search files for the pattern specified. The default action of the utility is to print the matches to the search. The *grep* utility can accept file-names to search or it can search data from standard input. This utility is used with the following syntax:

```
grep [options [e searchpattern] [-f filename]]
```

This utility is used with three variants controlled by the options shown in Table 4-20.

**Table 4-20**
**Options Used with grep**

| Option | Use |
| :--- | :--- |
| -G | The default behavior which interprets the pattern as a basic regular expression. |
| -E | Interprets the pattern as an extended regular expression. This option functions the same as the \-G option with GNU grep. |
| -F | Interprets the pattern as a list of fixed strings. |