# 172

# cpio

# Operands

+   directory A path name of an existing directory to be used as the target of cpio -p.

+   pattern Expressions making use of sb(1) of a pattern-matching notation similar to that used by the shell (see sb(1)) for file-name pattern matching and similar to regular expressions. The following metacharacters are defined:

+   * Match any string, including the empty string.

+   ? Match any single character.

+   [...] Match any one of the enclosed characters. A pair of characters separated by a dash (-) matches any symbol between the pair (inclusive), as defined by the system default collation sequence. If the first character following the opening [ is a !, the results are unspecified.

+   ! Don't match. (For example, the !abc* pattern excludes all files that begin with abc.)

In patterns, metacharacters ?, *, and [...] match the slash (/) character, and backslash (\) is an escape character. multiple cases of patternrand, if no pattern is specified, the default for patternis (that is, select all files).

Enclose each file in double quotes; otherwise, the name of a file in the current directory might be used.

# Usage

logfile(5) for the description of the behavior of cpio when encountering files greater than or equal to 2 Gbytes (231 bytes).

# Examples

The following example lists files and pipes the output to cpio -o so it can be directed (>) to a single file (~newfile). The -c option ensures that the file is portable to other machines (with the -H option).

```
ls | cpio -oc > ~newfile
```

Instead of ls, you could use find1), echo(1), cat(1), and so on, to pipe a list of names to cpio. You could redirect the output to a directory instead of a file.

The following example of cpio -1 uses the output file of cpio -o directed through a pipe with cat in the example below, extracts those files that match the patterns (memo/al, memo/b*), creates directories below the current directory as needed (-d option), and puts the files in the appropriate directories. The -c option if the input file was created with a portable header. If no patterns are given, all files from newfile are put in the directory.

```
cat @newfile | cpio -icd "memo/a**"
```

The following example of cpio -p takes the files named to it and copies them (-1 option) to another directory (newdir). The -d option creates directories as needed. The -m option retains the modification time.

```
find -depth -print | cpio -pdlwm newdir
```