# **OPTIONS**

**Ignore blank lines**
The `-B` (`--ignore-blank-lines`) option ignores differences that involve only blank lines. See also “Ignore whitespace at end of lines” (following) and “Ignore whitespace” (next page).

**Ignore whitespace at end of lines**
The `-b` (`--ignore-space-change`) option ignores whitespace (SPACES and TABS) at the ends of lines and considers other strings of whitespace (such as multiple SPACES or TABS) to be equal. See also “Ignore blank lines” (preceding) and “Ignore whitespace” (next page).

**Context**
The `-C` [*lines*] (`--context[=lines]`) option displays the sections of the two files that differ, including *lines* lines (the default is 3) around each line that differs to show the context. Each line in the first file that is missing from the second file is preceded by a hyphen (`-`); each extra line in the second file is preceded by a plus sign (`+`); and lines that have different versions in the two files are preceded by an exclamation point (`!`). When lines that differ are within *lines* lines of each other, they are grouped together in the output.

**Ignore case Unified**
The `-i` (`--ignore-case`) option ignores differences in case when comparing files.
The `-U` [*lines*] or `-u` (`--unified[=lines]`) option uses the easier-to-read unified output format. The *lines* argument is the number of lines of context; the default is three. The `-u` option does not take an argument and provides three lines of context.
This option first displays two lines that indicate which of the files you are comparing will be denoted by a plus sign (+) and which by a minus sign (-). In the following example, a minus sign indicates the colors.1 file; a plus sign indicates the colors.2 file.

```
$ diff -u colors.1 colors.2
--- colors.1	2014-04-05 10:12:12.322528610 -0700
+++ colors.2	2014-04-05 10:12:18.420531033 -0700
@@ -1,6 +1,5 @@
 red
+blue
 green
 yellow
-pink
-purple
 orange
```

The `diff -u` command breaks long, multiline text into *hunks*. Each hunk is preceded by a line starting and ending with two at signs (`@@`). This hunk identifier indicates the starting line number and the number of lines from each file for this hunk. In the example, the hunk covers the section of the `colors.1` file (indicated by a minus sign) from the first line through the sixth line. The `+1,5` indicates the hunk covers `colors.2` from the first line through the fifth line.
Following these header lines, `diff -u` displays each line of text with a leading minus sign, a leading plus sign, or a SPACE. A leading minus sign indicates the line occurs only in the file denoted by the minus sign. A leading plus sign indicates the line occurs only in the file denoted by the plus sign.