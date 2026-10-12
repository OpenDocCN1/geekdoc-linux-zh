Three types of change commands exist. Each type consists of a line number or comma-separated range of lines in the first file, a single character indicating the kind of change to make, and a line number or comma-separated range of lines in the second file. All line numbers are the original line numbers in each file. The following are the types of change commands:

+   l a r . Add the lines in range r of the second file after line 1 of the first file. For example, 8 a 12,15 means append lines 12–15 of file 2 after line 8 of file 1; or, if changing file 2 into file 1, delete lines 12–15 of file 2.

+   f c t . Replace the lines in range f of the first file with lines in range t of the second file. This is like a combined add and delete, but more compact. For example, 5 , 7 c 8,10 means change lines 5–7 of file 1 to read as lines 8–10 of file 2; or, if changing file 2 into file 1, change lines 8–10 of file 2 to read as lines 5–7 of file 1.

+   r d l . Delete the lines in range r from the first file; line 1 is where they would have appeared in the second file had they not been deleted. For example, 5 , 7 d 3 means delete lines 5–7 of file 1; or, if changing file 2 into file 1, append lines 5–7 of file 1 after line 3 of file 2.

For example, if a . t x t contains

```
a
b
c
d
e
```

and b . t x t contains

```
c
d
e
f
g
```

the diff command produces the following output:

```
1 , 2 d 0
< a
```