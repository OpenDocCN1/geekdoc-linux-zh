# Useful Linux Commands

APPENDIX A

941

TABLE A.4 diff Options
| **Option** | **Explanation** |
| :--- | :--- |
| `-b` | Causes **diff** to ignore changes in the amount of whitespace. |
| `-c` | Produces the "context **diff**" format. |
| `-i` | Causes **diff** to ignore differences in case—upper- and lowercase letters are treated the same. |
| `-q` | Causes **diff** only to report whether or not files differ; it does not print details of the differences. |
| `-r` | Causes **diff** to recursively compare subdirectory trees. Files in one tree are compared against the corresponding files in the other tree. |
| `-y` | Causes **diff** to print the differences in a "side-by-side" format. You need a large terminal window for this format to be easy to read. |

**diff** has many more options and features; consult **diff** (1) for more details.

If you want to compare English text, the **wdiff** program may produce easier-to-read output. It compares the words in two files. The following is an example:

```
$ wdiff file1 file2
```

```
Here is some text.  {+Ouch.+}
Here is a line.
[-Here is another line.-]
Yet another line.
{+foo bar.+}
```

New text is surrounded by {+...+} and deleted text by [--...-]. For more details, see **wdiff** (1).

# **Background Material**

**diff** is a standard UNIX program; **wdiff** is a GNU-specific program.

# # Regular Expressions

Regular expressions are special patterns that match pieces of text. Regular expressions are pervasive in UNIX; many text-processing commands use regular expression matching, and they are an important part of scripting languages, such as Perl and Tcl. Regular expressions are widely used for powerful text searching and processing. You can quickly perform many otherwise tedious text transformations using regular expressions.

![](bbox=[0.88, 0.28, 0.96, 0.43])