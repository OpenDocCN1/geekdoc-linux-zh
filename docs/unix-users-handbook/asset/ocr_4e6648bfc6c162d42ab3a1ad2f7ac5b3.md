-o output

The argument given is the name of an output file to use instead of the standard output. This file can be the same as one of the input files.

-u

Unique: suppress all but one in each set of lines having equal keys. If used with the -c option, check to see that there are no lines with duplicate keys, in addition to checking that the input file is sorted.

-y [kmem]

The amount of main memory used by the sort can have a large impact on its performance. If this option is omitted, sort begins using a system default memory size, and continues to use more space as needed. If this option is presented with a value, kmem, sort starts using that number of kilobytes of memory, unless the administrative minimum or maximum is violated, in which case the corresponding extremum will be used. Thus, -y 0 is guaranteed to start with minimum memory. By convention, -y (with no argument) starts with maximum memory.

-z recsz

The size of the longest line read is recorded in the sort phase so that buffers can be allocated during the merge phase. If the sort phase is omitted via the -c or -m options, a popular system default size will be used. Lines longer than the buffer size will cause sort to terminate abnormally. Supplying the actual number of bytes in the longest line to be merged (or some larger value) will prevent abnormal termination.

-T dir

Use dir as the directory for temporary scratch files rather than the default directory, which is is one of the following, tried in order: the directory as specified in the TMPDIR environment variable; /var/tmp, and finally, /tmp.

# Ordering Rule Options

When ordering options appear before restricted sort key specifications, the ordering rules are applied globally to all sort keys. When attached to a specific sort key (described below), the ordering options override all global ordering options for that key.

The following options override the default ordering rules:

-d

Quasi-dictionary order: only alphanumerics characters and blanks (spaces and tabs), as defined by LC_CTYPE are significant in comparisons (see environ(5)).

(XPG4 only.) The behavior is undefined for a sort key to which -i or -n also applies.

-f

Fold letters. Prior to being compared, all lowercase letters are effectively converted into their uppercase equivalents, as defined by LC_CTYPE.

-i

In non-numeric comparisons, ignore all characters which are non-printable, as defined by LC_CTYPE. For the ASCII character set, octal character codes 001 through 037 and 0177 are ignored.

-n

The sort key is restricted to an initial numeric string consisting of optional blanks, an optional minus sign, zero or more digits with optional radix character, and optional thousands separators.