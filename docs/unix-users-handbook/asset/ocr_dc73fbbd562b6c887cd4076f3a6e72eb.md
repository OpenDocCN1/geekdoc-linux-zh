# find

**find** - Recursively descends a directory structure looking for the file(s) listed.

Some commonly used options follow:

+   -   -f Specifies a file hierarchy for **find** to traverse.
-   -s When symbolic links are encountered, the file referenced by the link and not the link itself will be used.
-   -x Doesn't descend into directories that have a device number different from that of the file from which the descent began.
-   -print Prints pathname to standard output.
-   -size n True if the file's size is n.