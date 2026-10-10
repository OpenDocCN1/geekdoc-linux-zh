# The diff Command (Comparing)

| Option | Action | Comments |
| :--- | :--- | :--- |
| ▼ -y | Displays results in two | |
| ▼ --side-by-side | columns. | |
| ▼ -r | Includes sub-direcro- | |
| ▼ --recursive | ries when comparing | |
| | directories. | |
| ▼ -q | Only displays whether | |
| ▼ --brief | files differ. | |
| ▼ -S FILE | Only displays when files | |
| ▼ --report-identical-file | do not differ. | |

# Comparing Three Files: Using the diff3 Command

The diff3 command compares three files, and reports on the differences
between them. It does not give detailed information about the differences,
the way that diff does. diff3 can also be used to merge files using a simple
script (see the man pages for more detail).

Type: diff3 options 1st_file 2nd_file 3rd_file.

Two results may display:

+   ▼ === All three files differ