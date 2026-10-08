
processing of LC_MESSAGES.

## International Code Set Support

Single- and multi-byte character code sets are supported.

## EXAMPLES

Make a simple substitution in a file from the command line or from a shell script, changing abc to xyz:

```bash
sed 's/abc/xyz/' file1 >file.out
```

Same as above but use shell or environment variables var1 and var2 in search and replacement strings:

```bash
"sed \"s/$var1/$var2/\" file1 >file.out" or
```

```bash
sed 's/'$var1'/'$var2'' file1 >file.out
```

Multiple substitutions in a single command:

```bash
sed -e 's/abc/xyz/' -e 's/lmn/rst/' file1
```

```bash
"or" "sed -e 's/abc/xyz/' \\ -e 's/lmn/rst/' \\ file1 >file.out"
```

## WARNINGS

sed limits command scripts to a total of not more than 100 commands.

The hold space is limited to 8192 characters.

sed processes only text files. See the glossary for a definition of text files and their limitations.

## AUTHOR

sed was developed by OSF and HP.

## SEE ALSO

awk(1), ed(1), grep(1), environ(5), lang(5), regexp(5).

sed: A Non-Interactive Streaming Editor tutorial in the Text Processing Users Guide.

## STANDARDS CONFORMANCE

sed: SVID2, SVID3, XPG2, XPG3, XPG4, POSIX.2

## sort

![](img/75f39fc91296b889c0653851accdfd46_705_0.png)

sort - Sort contents of files.

sort(1)

sort(1)

### NAME

sort - sort or merge files

### SYNOPSIS

```bash
sort [-m] [-o output] [-bdfinruM] [-t char] [-k keydef] [-y [kmem]] [-z recsz] [-T dir] [file ...]
sort [-C] [-AdbfinruM] [-t char] [-k keydef] [-y [kmem]] [-z recsz] [-T dir] [file ...]
```

### DESCRIPTION

sort performs one of the following functions:

- 1. Sorts lines of all the named files together and writes the result to the specified output.
- 2. Merges lines of all the named (presorted) files together and writes the result to the specified output.
- 3. Checks that a single input file is correctly presorted.

The standard input is read if - is used as a file name or no input files are specified.

Comparisons are based on one or more sort keys extracted from each line of input. By default, there is one sort key, the entire input line. Ordering is lexicographic by characters using the collating sequence of the current locale. If the locale is not specified or is set to the POSIX locale, then ordering is lexicographic by bytes in machine-collating sequence. If the locale includes multi-byte characters, single-byte characters are machine-collated before multi-byte characters.

Behavior Modification Options

The following options alter the default behavior:

- -A
  Sorts on a byte-by-byte basis using each character's encoded value. On some systems, extended characters will be considered negative values, and so sort before ASCII characters. If you are sorting ASCII characters in a non-C/POSIX locale, this flag performs much faster.

- -c
  Check that the single input file is sorted according to the ordering rules. No output is produced; the exit code is set to indicate the result.

- -m
  Merge only; the input files are assumed to be already sorted.

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

## Ordering Rule Options

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

radix and thousands separator characters are defined by `LC_NUMERIC`. The field is sorted by arithmetic value. An empty (missing) numeric field is treated as arithmetic zero. Leading zeros and plus or minus signs on zeros do not affect the ordering. The `-n` option implies the `-b` option (see below).

- -r
  Reverse the sense of comparisons.

- -M
  Compare as months. The first several non-blank characters of the field are folded to uppercase and compared with the `langinfo(5)` items `ABMON_1` < `ABMON_2` < ... < `ABMON_12`. An invalid field is treated as being less than `ABMON_1` string. For example, American month names are compared such that `JAN` < `FEB` < ... < `DEC`. An invalid field is treated as being less than all months. The `-M` option implies the `-b` option (see below).

## Field Separator Options

The treatment of field separators can be altered using the options:

- -t char
  Use `char` as the field separator character; `char` is not considered to be part of a field (although it can be included in a sort key). Each occurrence of `char` is significant (for example, `<char><char>` delimits an empty field). If `-t` is not specified, `<blank>` characters will be used as default field separators; each maximal sequence of `<blank>` characters that follows a non-`<blank>` character is a field separator.

- -b
  Ignore leading blanks when determining the starting and ending positions of a restricted sort key. If the `-b` option is specified before the first `-k` option (`+pos` argument), it is applied to all `-k` options (`+pos` arguments). Otherwise, the `-b` option can be attached independently to each `-k` field start or field end option (`+pos1` or `-pos2` argument; see below). Note that the `-b` option is only effective when restricted sort key specifications are given.

## Restricted Sort Key

- -k keydef
  The `keydef` argument defines a restricted sort key. The format of this definition is

  `field_start[type] [,field_end[type]]`

  which defines a key field beginning at `field_start` and ending at `field_end`. The characters at positions `field_start` and `field_end` are included in the key field, providing that `field_end` does not precede `field_start`. A missing `field_end` means the end of the line. Fields and characters within fields are numbered starting with 1. Note that this is different than the obsolete form of restricted sort keys, where numbering starts at 0. See `WARNINGS` below.

Specifying field start and field end involves the notion of a field, a minimal sequence of characters followed by a field separator or a new-line. By default, the first blank of a sequence of blanks acts as the field separator. All blanks in a sequence of blanks are considered to be part of the next field; for example, all blanks at the beginning of a line
