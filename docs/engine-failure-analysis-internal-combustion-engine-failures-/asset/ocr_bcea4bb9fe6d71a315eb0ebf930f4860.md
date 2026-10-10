# ## rev

*rev* [ *filename* ]

Reverse the order in which characters appear on each line of the specified filename. You can specify more than one filename in a space-separated list or by using a shell pattern (see the section “Shell Patterns” in Chapter 4).

*See also* tac.

# ## sdiff

*sdiff* [ *option* ] *filename-1 filename-2*

Launches an interactive utility that enables you to compare two sorted files (*filename-1* and *filename-2*). See *sort* for information on sorting files. The program shows the differences between the two files in two side-by-side columns. To compare non-sorted text files, use *diff*.

*See also* cmp, comm, diff, diff3.

# OPTIONS

| Use This Option | To Do This |
| --- | --- |
| -a | Treat all files as text and compare them line by line |
| -B, --ignore-blank-lines | Ignore changes that insert or delete blank lines |
| -b, --ignore-space-change | Ignore changes involving white space |
| -i, --ignore-case | Ignore changes in case |
| -I regexp, --ignore-matching-lines=regexp | Ignore changes that insert or delete lines matching *regexp* (regular expression) |