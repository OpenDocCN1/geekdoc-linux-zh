If set, *git diff* uses a prefix pair that is different from the standard “a/” and “b/” depending on what is being compared. When this configuration is in effect, reverse diff output also swaps the order of the prefixes:

+   git diff  
+       compares the (i)ndex and the (w)ork tree;
+   git diff HEAD  
+       compares a (c)ommit and the (w)ork tree;
+   git diff —cached  
+       compares a (c)ommit and the (i)ndex;
+   git diff HEAD:file1 file2  
+       compares an (o)bject and a (w)ork tree entity;
+   git diff —no-index a b  
+       compares two non-git things (1) and (2).

# diff.noprefix

If set, *git diff* does not show any source or destination prefix.

# diff.orderFile

File indicating how to order files within a diff, using one shell glob pattern per line. Can be overridden by the *-O* option to (1).

# diff.renameLimit

The number of files to consider when performing the copy/rename detection; equivalent to the *git diff* option *-L*.

# diff.renames

Tells Git to detect renames. If set to any boolean value, it will enable basic rename detection. If set to “copies” or “copy”, it will detect copies, as well.

# diff.suppressBlankEmpty

A boolean to inhibit the standard behavior of printing a space before each empty output line. Defaults to *false*.

# diff.submodule

Specify the format in which differences in submodules are shown. The “log” format lists the commits in the range like (1)summary does. The “short” format format just shows the names of the commits at the beginning and end of the range. Defaults to *short*.

# diff.wordRegex

A POSIX Extended Regular Expression used to determine what is a “word” when