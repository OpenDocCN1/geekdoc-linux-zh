# 1296

# sort

# /usr/xpg4/bin/sort

-c Same as /usr/bin/sort, except produce no output under any circumstances.

-m Merge only. Assume the input files are already sorted.

-u Sort uniquely by suppressing all but one in each set of lines having equal keys. If used with the -c option, check that there are no lines with duplicate keys, in addition to checking that the input file is sorted.

-o output Specify the name of an output file to be used instead of the standard output. This file can be as one of the input files.

-S kmem Specify the maximum amount of swap-based memory for sorting, in kilobytes (the default unit). You can also specify kmem directly as a number of bytes (b), kilobytes (k), megabytes (m), gigabytes (g), or terabytes (t), or as a percentage (%) of the available physical memory.

You can tune performance for a specific scenario with the -S option. However, you should note in particular that sort has greater knowledge of how to use a finite amount of memory for sorting than does the virtual memory system. Thus, a sort invoked to request an extremely large amount of memory with the -S option performs poorly. New in the Solaris 8 release.

-T directory Specify the name of a directory to use for temporary files. (Obsolete with the Solaris 8 release.) Specify the amount of main memory used initially. Start using that number of kilobytes unless the administrative minimum or maximum is exceeded, in which case you use the corresponding extremus. Thus, -y 0 is guaranteed to start with minimum memory.-y no kmemargument starts with maximum memory. If you omit this option, begin using a system default memory and continue to use more space as needed.

-z recsz (Obsolete.) Use to prevent termination when lines longer than the system-dependent buffer size are encountered. Because sort automatically allocates buffers large enough to hold the longest line, this has no effect.

# Ordering Options

The default sort order depends on the value of LC_COLLATE. If LC_COLLATE is set to C, sorting is in ASCII order. If LC_COLLATE is set to en_US, sorting is case insensitive when the two strings are equal and if one an uppercase letter earlier than the other. Other locales have none.

The following options override the default ordering rules. When ordering options appear independently of any key field specifications, the requested field ordering rules are applied globally to all sort keys. When attached to a specific key, the specified ordering options override global ordering options for that key. In the obsolete