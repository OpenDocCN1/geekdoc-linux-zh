# 104

# bdiff — Big diff

# Synopsis

/usr/bin/bdiff filename filename2 [n] [-s]

# Description

bdiff is similar to diff, except that you can use it to process files that are too large for diff. A large file is a regular file whose size is greater than or equal to 2 Gbytes (**31 bytes). A small file is a regular file whose size is less than 2 Gbytes.
If filename(filename)~, the standard input is read.
bdiff ignores lines common to the beginning of both files, splits the remainder of each file into n line segments, and invokes diff on corresponding segments. If both optional arguments are specified, you must use them in the order indicated above.
The output of bdiff is exactly that of diff, with line numbers adjusted to make it as if the files have been processed as one. The first part of the bdiff output lists the line numbers that differ in the two files, separated by c for changed. Lines from the first file are marked with <, and lines from the second file are marked with >.

> Note — Because of the segmentation of the files, bdiff does not necessarily find a smallest sufficient set of differences.

# Options

+   - n Specify the number of line segments. By default, the value of n is 3500. This option is useful in cases where 3500-line segments are too large for diff, causing it to fail.
- s Do not print bdiff diagnostics (silent option). This option does not suppress possible diagnostic messages from diff, which bdiff calls.

# Usage

Use largefile(5) for the description of the behavior of bdiff when encountering files greater than or equal to 2 Gbytes (**31 bytes).

# Examples

In the following example, two (small) files are first displayed by the cat command, and then bdiff compares the two files. You can use bdiff on small files; however, diff has more options for comparing small files.

```
castle@ kookaburra1
kookaburra sits in the old gum tree
Merry king of the bush is
Laugh, kookaburra, laugh
Your life must be.

kookaburra sits in the old gum tree
Eating all the gumdrops he can see
Laugh, kookaburra, laugh
Leave some there for me.
castle@ cat kookaburra2
kookaburra sits in the old gum tree
```