![](bbox=[0.23, 0.09, 0.86, 0.38])

# PATHNAMES

Every file has a *pathname*, which is a trail from a directory through part of the directory hierarchy to an ordinary file or a directory. Within a pathname, a slash (/) following (to the right of) a filename indicates that the file is a directory file. The file following (to the right of) the slash can be an ordinary file or a directory file. The simplest pathname is a simple filename, which points to a file in the working directory. This section discusses absolute and relative pathnames and explains how to use each.

# ABSOLUTE PATHNAMES

/ (root) The root directory of the filesystem hierarchy does not have a name; it is referred to as the *root directory* and is represented by a / (slash) standing alone or at the left end of a pathname.

An absolute *pathname* starts with a slash (/), which represents the root directory. The slash is followed by the name of a file located in the root directory. An absolute pathname can continue, tracing a path through all intermediate directories, to the file identified by the pathname. String all the filenames in the path together, following each directory with a slash (/). This string of filenames is called an absolute pathname because it locates a file absolutely by tracing a path from the root directory to the file. Typically the absolute pathname of a directory does not include the trailing slash, although that format may be used to emphasize that the pathname specifies a directory (e.g., /*home/zach*/). The part of a pathname following the final slash is called a *simple filename*, *filename*, or *basename*. Figure 6-5 shows the absolute pathnames of directories and ordinary files in part of a filesystem hierarchy.