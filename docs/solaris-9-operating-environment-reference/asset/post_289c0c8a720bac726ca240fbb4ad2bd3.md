
## Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNWmnisu |

## See Also

ypfiles(4), attributes(5)

## zcat — Compress, Uncompress Files or Display Expanded Files

### Synopsis
/usr/bin/zcat [file...]

### Description

See compress(1).

## zip, zipcloak, zipnote, zipsplit — Package and Compress (Archive) Files

### Synopsis

```
zip [-aABcDDeEfFghjklLMmoqrRSTuvWxyz!$] [-b path] [-n suffixes]
  [-t mmddyyyy] [-tt mmddyyyy] [zipfile [file1 file2...]] [-xi list]
zipcloak [-dhL] [-b path] zipfile
zipnote [-hwL] [-b path] zipfile
zipsplit [-hiLPst] [-n size [-b path] zipfile
```

## 1580

## zip, zipcloak, zipnote, zipsplit

### Description

The zip command, new in the Solaris 8 release, is a compression and file packaging command for UNIX, VMS, MS-DOS, OS/2, Windows NT, Minix, Atari, Macintosh, Amiga, and Acorn RISC OS.

zip is analogous to a combination of the UNIX commands tar(1) and compress(1) and is compatible with PKZIP (Phil Katz's for MS-DOS systems).

Note — Source for zip is available in the SUN package.

A companion program, unzip(1), unpacks archives. The zip and unzip(1) programs can work with archives produced by PKZIP, and PKZIP and PKUNZIP can work with archives produced by zip. zip version 2.3 is compatible with PKZIP 2.04. Note PKUNZIP 1.10 cannot extract files produced by PKZIP 2.04 or zip 2.3. You must use UNZIP 2.04 or unzip 5.1(or later versions) to extract them.

For help on zip and unzip, run without specifying any parameters on the command line.

zip is useful for packing a set of files for distribution, archiving files, and saving disk space by temporarily compressing unused files or directories.

The zip program puts one or more compressed files into a single zip archive, along with information about the files (name, path, date, time of last modification, protection, and check information to verify integrity). An entire directory structure can be packed into a zip archive with a single command. Compression ratios of 2:1 to 3:1 are common for text files. zip has one compression method (deflation) and can also store files without compression. zip automatically chooses the best of the two for each file to be compressed.

When given the name of an existing archive, zip replaces identically named entries in the zip archive or adds entries for new names. For example, if foo.zip exists and contains foo/file and foo/file2, the directory contains the files foo/file1 and foo/file3,

```
zip -r foo foo
```

replaces foo in foo.zip and adds foo/file3 to foo.zip. After this, foo.zip contains foo/file1, foo/file2, and foo/file3, with foo/file2 unchanged before.

If the list is specified as - [Not on MacOS] zip takes the list of input files from standard input. Under UNIX, you can use this option to powerful effect in conjunction with the find(1) command. The following example shows all the C source files in the current directory and its subdirectories.

```
find -name "*.c" -print | zip source @
```

Note that you must quote the filename to keep the shell from expanding it. zip also accepts a single dash (-) as the zipfilename, in which case it writes the zipfile to standard output, enabling you to pipe the output to another program. The following example writes the zip output directly to a tape with the specified block size to back up the current directory.

```
zip -r | dd of=/dev/nrst0 bs=16k
```

zip also accepts a single dash (-) as the name of a file to be compressed. It reads the file from standard input, enabling zip to take input from another program. The following example compresses the output of the tar command to back up the current directory.

## zip, zipplok, zipnote, zipsplit 1581

```
tar cf - | zip backup -
```

This command generally produces better compression than the previous example with the -r option because zip can take advantage of redundancy between files. You can restore the backup with the following command.

```
unzip -p backup | tar xf -
```

When you specify no zipfilename and standard output is not a terminal, zip acts as a filter, compressing standard input to standard output. The following example

```
tar cf - | zip | dd of=/dev/nrst0 obs=16k
```

is equivalent to

```
tar cf - | zip - | dd of=/dev/nrst0 obs=16k
```

You can extract zip archives that are created in this way with the funzip command, which is provided in the unzip package or by gunzip, which is provided in the gzip package. The following example shows the syntax for extracting a zip archive with funzip.

```
dd if=/dev/nrst0 bs=16k | funzip | tar xvf
```

When changing an existing zip archive, zip writes a temporary file with the new contents and replaces the old one only when the process of creating the new version.

### Options

- -a: Add subdirectories to the archive.
- -A: Create self-extracting archive.
- -b: Use the specified path for temporary files.
- -c: Do not add a comment for files.
- -D: Do not create entries for directories.
- -E: Use EBCDIC formatting.
- -e: Encrypt with a password.
- -f: Specify the zip file.
- -g: Use a file for the comment.
- -h: Show help message.
- -i: Include only specified files.
- -J: Include only data-fork of files.
- -k: Preserve file attributes.
- -l: List contents of the archive.
- -L: Use long-format listing.
- -m: Move files after compressing.
- -n: Exclude files matching a pattern.
- -o: Do not overwrite existing files.
- -p: Preserve file permissions.
- -q: Quiet mode.
- -X: Delete extra-attributes from the archive.
- -r: Recursively process subdirectories.
- -s: Specify the compression method.
- -t: Test the archive integrity.
- -u: Update only changed files.
- -x: Exclude files matching a pattern.
- -z: Use compression.
- -B: Use the specified path for temporary files.
- -T: Use a file for the comment.
- -+: Add one-line comments for each file.
- -*: Delete entries from the archive.
- -0: Don't add delimiter.
- -1: Use LF rather than CR/LF as delimiter.
- -2: Space fill to maximum record length.
- -3: Trim trailing space.
- -8: Force 30K expand large files.
