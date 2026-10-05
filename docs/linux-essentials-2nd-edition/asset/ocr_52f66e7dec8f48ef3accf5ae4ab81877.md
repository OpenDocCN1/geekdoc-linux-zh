# Chapter 8 · Searching, Extracting, and Archiving Data

Of the options in Table 8.10, the -r option is probably the most important, at least if you want to compress an entire directory tree. If you fail to use this, your archive will contain no subdirectories. Given the speed of modern CPUs, using -9 on a regular basis also makes sense to achieve maximum compression.

To uncompress and extract files in a zip archive file, you can use the unzip program:

```
$ unzip archive.zip
```

This example uncompresses the files in the archive.zip file into the current directory. Like zip, unzip supports a large number of options, the most important of which appear in Table 8.11.

| TABLE 8.11 Common unzip options |
| Option | Description |
| --- | --- |
| -f | Freshens files from the archive; that is, extracts only those files that exist on the main filesystem and that are newer in the archive than on the main filesystem |
| -l | Lists files in the archive but does not extract |
| -p | Extracts files to a pipeline |
| -t | Tests the integrity of files in the archive |
| -u | Updates files; similar to -f, but also extracts files that don't exist on the filesystem |
| -v | Lists files in the archive in a more verbose format than -l |
| -L | Converts filenames to lowercase if they originated on an uppercase-05, such as DOS |
| -n | Never overwrites existing files |
| -o | Overwrites existing files without prompting |

As a general rule, using unzip without any options except for the input file works well. However, you might want to use one or more of its options on occasion. The -l option is particularly useful for examining the archive's contents without extracting it.