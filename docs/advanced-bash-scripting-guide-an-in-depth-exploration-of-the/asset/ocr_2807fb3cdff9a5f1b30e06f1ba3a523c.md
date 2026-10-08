# Advanced Bash-Scripting Guide

```
# Note that the options pax must be in the correct order --
+# pax -fw    has an entirely different effect.

pax -f daily_backup.p
# Lists the files in the archive.

pax -rf daily_backup.p /bsd-server/files
# Restores the backed-up files from the Linux machine
# onto a bsd one.
```

Note that pax handles many of the standard archiving and compression commands.

# Compression

# gzip

The standard GNU/UNIX compression utility, replacing the inferior and proprietary compress. The corresponding decompression command is gzip, which is equivalent to gzip -d.

+   - The -c option selects the output of gzip to stdout. This is useful when piping to other commands.

The zcat compresses a gzipped file to stdout, as possible input to a pipe or redirection. This is, in effect, a cat command that compresses files (including files processed with compress utility). The zcat is equivalent to gzip -dc.

+   - On some common UNIX systems, zcat is a synonym for uncompress -c, and will not work on gzipped files.
See also Example 7-7.

# zip2

An alternate compression utility, usually more efficient (but slower) than gzip, especially on large files. The decompression command is bunzip2.

Similar to the zcat command, bcat decompresses a bzipped2-ed file to stdout.

+   - Newer versions of tar have been patched with zip2 support.

# compress, uncompress

This is an older, proprietary compression utility found in commercial UNIX distributions. The more efficient gzip has largely replaced it. Linux distributions generally include a compress workalike for compatibility, although gzip can unarchive files treated with compress.

+   - The znew command transforms compressed files into gzipped ones.

# sq

Yet another compression (squeeze) utility, a filter that works only on sorted ASCII lists. It uses the standard syntax for a filter, sq < input-file > output-file. But not as fast as gzip. The corresponding decompression filter is unsq, invoked like sq.

+   - The output of sq may be piped to gzip for further compression.

# zip, unzip

Cross-platform file archiving utility compatible with DOS pkzip.exe, "Zipped archives seem to be a more common medium of file exchange on the Internet using "tarballs."

Chapter 16. External Filters, Programs and Commands