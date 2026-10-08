# diff 255

Produce a script of only a, c, and d commands for the editor, which recreates file2 from file. In connection with -e, the following shell program may help maintain multiple versions of a file. Only an ancestral file ($1) and a chain of version-to-version ed scripts ($2,$3,...) made by diff need be on hand. A latest version appears on the standard output.

-e

(shift; cat $; echo '$1,$sp') | ed - $1
In rare circumstances, diff finds a smallest sufficient set of file differences.

Produce a script similar to -e in the opposite order. Not useful with ed.
A fast, heart-joyed job. This works only when changed stretches are short and well separated but does on files of unlimited length. Options -c, -e, and -n are unavailable with -h.
diff does not descend into directories with this option.

-h

Produce a script similar to -e, but in the opposite order and with
counted lines identical to each insert or delete command.

-n

List differences with three lines of context. The output is similar to the
-c option except that the context is unified. Removed and changed
lines in file1 are marked with a-; lines added or changed in file2
are marked with a +. Both versions of changed lines are shown in the
output. Added, removed, and context lines are shown only once.
The identification of file1 and file2 is different, with --- used instead of
n-c option *** and +++ instead of the -c option ---. Each option is
separated by a line of the following form.

-u

```
@@ -n1,n2+n3,n4 @@
```

This option is new in the Solaris 9 release.

-U

List differences in the same way as the -u option with numbered lines
of context. This option is new in the Solaris 9 release.

The options for the diff command are used to compare directories.

Produce output in long format. Before the diff, pipe each text file
through pr(1) to paginate it. Remember other differences and
summarize them after all text differences are reported.

-l

Apply diff recursively to compare subdirectories encountered.

-r

Report files that are the identical; these would not otherwise be
mentioned.

-S name

Start a directory diff in the middle, beginning with the file name.

# Operands

file1

A path name of a file or directory to be compared. If either file or
file2 is -, use the standard input in its place.

file2

directory1

A path name of a directory to be compared.

directory2