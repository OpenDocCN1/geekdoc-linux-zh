# Specifying patterns using regular expressions

Regular expressions provide a convenient and consistent way of specifying patterns to be matched. Regular expressions are similar to wildcards, but are much more powerful, providing a wider scope of pattern selecting. Several different Linux commands use regular expressions, including ed, sed, awk, grep, and, to a limited extent, vi and emacs.

The special characters in Table 9-3 are typical of regular expressions in general. Once you understand these special characters, you need to learn only a few variations as they arise.

Table 9-3 Special Characters for Regular Expressions

| Symbol | Meaning |
|---|---|
| . | Matches any single character except newline. |
| * | Matches zero or more of the preceding characters. |
| ^ | Matches the beginning of a line. |
| $ | Matches the end of a line. |
| \< | Matches the beginning of a word. |
| \> | Matches the end of a word. |
| [ ] | Matches one of the enclosed characters or range of characters |
| [^] | Matches any characters not enclosed |
| \ | Take the following symbol literally |

Within a regular expression, any character that does not have a special meaning stands for itself. For example, to search for lines that contain the word “foo” in the file data.txt, you would use the following command:

```
grep foo data.txt
```

To search only for lines in data.txt that begin with the word “foo,” you would use the following command instead:

```
grep '^foo' data.txt
```