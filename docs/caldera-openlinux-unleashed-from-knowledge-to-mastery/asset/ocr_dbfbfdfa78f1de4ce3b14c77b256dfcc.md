The 3d2 indicates that line 3 of the original file should be deleted. The deleted line is shown preceded by <.

The 4a4 indicates that a line should be added after line 4, and the new line is shown preceded by >.

You can produce a more readable format by using the -c option. The following produces a so-called context diff:

```
$ diff -c file1 file2

***file1	Mon Jun 28 10:09:49 1999
---file2	Mon Jun 28 10:09:46 1999
******
***1,4****
! Here is some text.
! Here is a line.
- Here is another line.
- Yet another line.
---1,4 ----
! Here is some text.  Ouch.
! Here is a line.
! Yet another line.
+ fooo bar.
```

A context diff has the following format:

+   • Three asterisks followed by the first filename and its date of modification.
+   • Three dashes followed by the second filename and its date of modification.
+   • A line of 15 asterisks.
+   • Blocks of changes.

Each block of changes has the following format:

+   • Three asterisks, followed by the starting and ending line of the block in the first file, followed by four asterisks.
+   • Lines from the first file. Changed lines are flagged with !; deleted lines are flagged with -, and unchanged lines are not flagged.
+   • Three dashes, followed by the starting and ending line of the block in the second file, followed by four dashes.
+   • Lines from the second file. Changed lines are flagged with !; additional lines are flagged with +, and unchanged lines are not flagged.

diff has a number of useful options. Table A.4 lists some of these.