# OPTIONS

**-a**, --all	Display counts for all files, not just directories.

**-b**, --bytes	Print sizes in bytes.

**-c**, --total	Write a grand total of all of the arguments after all arguments have been processed. This can be used to find out the disk usage of a directory, with some files excluded.

**-k**, --kilobytes	Print sizes in kilobytes. This overrides the environment variable POSIXLY_CORRECT.

**-l**, --count-links	Count the size of all files, even if they have appeared already in another hard link.

**-s**, --summarize	Display only a total for each argument.

**-x**, --one-file-system	Skip directories that are on different filesystems from the one that the argument being processed is on.

**-D**, --dereference-args	Dereference symbolic links that are command line arguments. Does not affect other symbolic links. This is helpful for finding out the disk usage of directories like /usr/tmp where they are symbolic links.

**-L**, --dereference	Dereference symbolic links (show the disk space used by the file or directory that the link points to instead of the space used by the link).

**-S**, --separate-dirs	Count the size of each directory separately, not including the sizes of subdirectories.

**--help**	Print a usage message on standard output and exit successfully.

**--version**	Print version information on standard output then exit successfully.

# BUGS

On BSD systems, **du** reports sizes that are half the correct values for files that are NFS-mounted from HP-UX systems. On HP-UX systems, it reports sizes that are twice the correct values for files that are NFS-mounted from BSD systems. This is due to a flaw in HP-UX; it also affects the HP-UX **du** program.