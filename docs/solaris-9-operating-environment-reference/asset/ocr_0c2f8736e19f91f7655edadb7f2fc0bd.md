# sdiff

Attributes
See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNcsu |
| CSI | Enabled |

See Also
attributes (5)

# sdiff — Print, Side-by-Side, Differences Between Two Files

Synopsis
/usr/bin/sdiff [-l] [-s] [-o output] [-w n] filename filename

Description
The diff command uses the output of the diff command to produce a side-by-side
listing of two files, indicating lines that are different.
Differences are shown in the following ways.

+   - A blank gutter is printed between the lines if they are identical.
- A < is shown in the gutter if the line appears only in filename1.
- A > is shown in the gutter if the line appears only in filename2.
- A ! is shown between the lines if they are different.

+   Options
-l Print only the left side of any lines that are identical.
-s Do not print identical lines.
-o output Use the output argument as the name of a third file that is created as
a merge of filename1 and filename2. Copy identical lines of
filename1 and filename2 to output. Print sets of differences as
produced by diff when a set of differences share a common gutter
character. After printing each set of differences, prompt with a #
wait for you to use one of the following commands.
-l Append the left column to the output file.
-r Append the right column to the output file.
-s Turn on silent mode; do not print identical lines.
-v Turn off silent mode.
-e Call the editor with the left column.
-r Call the editor with the right column.
-b Call the editor with the concatenation of left and right.