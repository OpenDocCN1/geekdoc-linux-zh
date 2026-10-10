-*wholename pattern*
See -ipath. This alternative is less portable than -ipath.

-*links n*
File has n links.

-*lname pattern*
File is a symbolic link whose contents match shell pattern *pattern*. The metacharacters do not treat `/` or `.` specially. If the -L option or the **follow** option is in effect, this test returns false unless the symbolic link is broken.

-*minmin n*
File's data was last modified n minutes ago.

-*mmin n*
File's data was last modified n*24 hours ago. See the comments for -atime to understand how rounding affects the interpretation of file modification times.

-*name pattern*
Base of file name (the path with the leading directories removed) matches shell pattern *pattern*. Because the leading directories are removed, the file names considered for a match with -name will never include a slash, so `-name a/b` will never match anything (you probably need to use -path instead). The metacharacters (`*`, `?`, and `[]`) match a `.` at the start of the base name (this is a change in findutils-4.2.2; see section STANDARDS CONFORMANCE below). To ignore a directory and the files under it, use -prune; see an example in the description of -path. Braces are not recognised as being special, despite the fact that some shells including Bash imbue braces with a special meaning in shell patterns. The filename matching is performed with the use of the **fnmatch(3)** library function. Don't forget to enclose the pattern in quotes in order to protect it from expansion by the shell.

-*newer file*
File was modified more recently than *file*. If *file* is a symbolic link and the -H option or the -L option is in effect, the modification time of the file it points to is always used.

-*newerXY reference*
Compares the timestamp of the current file with *reference*. The *reference* argument is normally the name of a file (and one of its timestamps is used for the comparison) but it may also be a string describing an absolute time. X and Y are placeholders for other letters, and these letters select which time belonging to how *reference* is used for the comparison.

+   a	The access time of the file *reference*
+   B	The birth time of the file *reference*
+   c	The inode status change time of *reference*
+   m	The modification time of the file *reference*
+   t	*reference* is interpreted directly as a time