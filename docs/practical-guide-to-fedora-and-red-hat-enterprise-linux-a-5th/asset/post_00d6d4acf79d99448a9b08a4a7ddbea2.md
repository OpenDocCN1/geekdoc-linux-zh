
# bzip2: COMPRESSES A FILE

The **bzip2** utility compresses a file by analyzing it and recoding it more efficiently. The new version of the file looks completely different. In fact, because the new file contains many nonprinting characters, you cannot view it directly. The **bzip2** utility works particularly well on files that contain a lot of repeated information, such as text and image data, although most image data is already in a compressed format.

The following example shows a boring file. Each of the 8,000 lines of the `letter_e` file contains 72 `e`'s and a `NEWLINE` character that marks the end of the line. The file occupies more than half a megabyte of disk storage.

```bash
$ ls -l
-rw-rw-r--   1 sam sam 584000 Mar  1 22:31 letter_e
```

The `-l` (long) option causes `ls` to display more information about a file. Here it shows that `letter_e` is 584,000 bytes long. The `--verbose` (or `-v`) option causes **bzip2** to report how much it was able to reduce the size of the file. In this case, it shrunk the file by 99.99 percent:

```bash
$ bzip2 -v letter_e
letter_e: 11680.0:1,  0.001 bits/byte, 99.99% saved, 584000 in, 50 out.
$ ls -l
-rw-rw-r--   1 sam sam 50 Mar  1 22:31 letter_e.bz2
```

Now the file is only 50 bytes long. The **bzip2** utility also renamed the file, appending `.bz2` to its name. This naming convention reminds you that the file is compressed; you would not want to display or print it, for example, without first decompressing it. The **bzip2** utility does not change the modification date associated with the file, even though it completely changes the file's contents.

In the following, more realistic example, the file `zach.jpg` contains a computer graphics image:

```bash
$ ls -l
-rw-r--r--   1 sam sam 33287 Mar  1 22:40 zach.jpg
```

The **bzip2** utility can reduce the size of the file by only 28 percent because the image is already in a compressed format:

```bash
$ bzip2 -v zach.jpg
zach.jpg:  1.391:1,   5.749 bits/byte, 28.13% saved, 33287 in, 23922 out.

$ ls -l
-rw-r--r--   1 sam sam 23922 Mar  1 22:40 zach.jpg.bz2
```

Refer to the **bzip2** man page, www.bzip.org, and the `Bzip2 mini-HOWTO` (see page 130) for more information.

# bunzip2 AND bcat: DECOMPRESS A FILE

You can use the `bunzip2` utility to restore a file that has been compressed with **bzip2**:

```bash
$ bunzip2 letter_e.bz2
$ ls -l
-rw-rw-rw- 1 sam sam 584000 Mar 1 22:31 letter_e
$ bunzip2 zach.jpg.bz2
$ ls -l
-rw-r-r-r-- 1 sam sam 33287 Mar 1 22:40 zach.jpg
```

The `bcat` utility displays a file that has been compressed with `bzip2`. The equivalent of `cat` for `.bz2` files, `bcat` decompresses the compressed data and displays the contents of the decompressed file. Like `cat`, `bcat` does not change the source file. The pipe in the following example redirects the output of `bcat` so that instead of being displayed on the screen it becomes the input to `head`, which displays the first two lines of the file:

```bash
$ bcat letter_e.bz2 | head -2
eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee
eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee
```

After `bcat` is run, the contents of `letter_e.bz2` is unchanged; the file is still stored on the disk in compressed form.

## bzip2recover

The `bzip2recover` utility supports limited data recovery from media errors. Give the command `bzip2recover` followed by the name of the compressed, corrupted file from which you want to try to recover data.

# gzip: Compresses a File

### gunzip and zcat
The `gzip` (GNU zip) utility is older and less efficient than `bzip2`. Its flags and operation are very similar to those of `bzip2`. A file compressed by `gzip` is marked by a `.gz` filename extension. Linux stores compressed pages in `gzip` format to save disk space; likewise, files you download from the Internet are frequently in `gzip` format. Use `gzip`, `gunzip`, and `zcat` just as you would use `bzip2`, `bunzip2`, and `bcat`, respectively. Refer to the `gzip` info page for more information.

### compress
The `compress` utility can also compress files, albeit not as well as `gzip`. This utility marks a file it has compressed by adding `.Z` to its name.

### gzip versus zip
**Tip:** Do not confuse `gzip` and `gunzip` with the `zip` and `unzip` utilities. These last two are used to pack and unpack `zip` archives containing several files compressed into a single file that has been imported from or is being exported to a system running Windows. The `zip` utility constructs a `zip` archive, whereas `unzip` unpacks `zip` archives. The `zip` and `unzip` utilities are compatible with PKZIP, a Windows program that compresses and archives files.

# tar: Packs and Unpacks Archives

The `tar` utility performs many functions. Its name is short for *tape archive*, as its original function was to create and read archive and backup tapes. Today it is used to create a single file (called a *tar file*, *archive*, or *tarball*) from multiple files or directory hierarchies and to extract files from a `tar` file. The `cpio` utility performs a similar function.

In the following example, the first `ls` shows the existence and sizes of the files `g`, `b`, and `d`. Next `tar` uses the `-c` (create), `-v` (verbose), and `-f` (write to or read from a file) options^2 to create an archive named `all.tar` from these files. Each line output displays the name of the file `tar` is appending to the archive it is creating.

The `tar` utility adds overhead when it creates an archive. The next command shows that the archive file `all.tar` occupies about 9,700 bytes, whereas the sum of the sizes of the three files is about 6,000 bytes. This overhead is more appreciable on smaller files, such as the ones in this example:

```bash
$ ls -l g b d
-rw-r--r--    1 jenny    jenny    1302    Aug    20    14:16    g
-rw-r--r--    1 jenny    other    1178    Aug    20    14:16    b
-rw-r--r--    1 jenny    jenny    3783    Aug    20    14:17    d
$ tar -cvf all.tar g b d
g
b
d
$ ls -l all.tar
-rw-r--r--    1 jenny    jenny    9728    Aug    20    14:17    all.tar
$ tar -tvf all.tar
-rw-r--r-- jenny/jenny        1302    2008-08-20    14:16    g
-rw-r--r-- jenny/other         1178    2008-08-20    14:16    b
-rw-r--r-- jenny/jenny        3783    2008-08-20    14:17    d
```

The final command in the preceding example uses the `-t` option to display a table of contents for the archive. Use `-x` instead of `-t` to extract files from a tar archive. Omit the `-v` option if you want `tar` to do its work silently.

You can use `bzip2`, `compress`, or `gzip` to compress tar files, making them easier to store and handle. Many files you download from the Internet will already be in one of these formats. Files that have been processed by `tar` and compressed by `bzip2` frequently have a filename extension of `.tar.bz2` or `.tbz`. Those processed by `tar` and `gzip` have an extension of `.tar.gz` or `.tgz`, whereas files processed by `tar` and `compress` use `.tar.Z` as the extension.

You can unpack a tarred and gzipped file in two steps. (Follow the same procedure if the file was compressed by `bzip2`, but use `bunzip2` instead of `gunzip`.) The next example shows how to unpack the `GNU make` utility after it has been downloaded from ftp.gnu.org/pub/gnu/make/make-3.80.tar.gz:

```bash
$ ls -l mak*
-rw-rw-r--    1 sam    sam    1211924    Jan    20    11:49    make-3.80.tar.gz
$ gunzip mak*
$ ls -l mak*
-rw-rw-r--    1 sam    sam    4823040    Jan    20    11:49    make-3.80.tar
```

> 2. Although the original UNIX `tar` did not use a leading hyphen to indicate an option on the command line, it now accepts hyphens. The GNU `tar` described here will accept `tar` commands with or without a leading hyphen. This book uses the hyphen for consistency with most other utilities.

```bash
$ tar -xvf mak* 
make-3.80/ 
make-3.80/po/ 
make-3.80/po/Makefile.in.in 
... 
make-3.80/tests/run_make_tests.pl 
make-3.80/tests/test_driver.pl
```

The first command lists the downloaded tarred and gzipped file: make-3.80.tar.gz (about 1.2 megabytes). The asterisk (*) in the filename matches any characters in any filenames (page 244), so you end up with a list of files whose names begin with make; in this case there is only one. Using an asterisk saves typing and can improve accuracy with long filenames. The gunzip command decompresses the file and yields make-3.80.tar (no .gz extension), which is about 4.8 megabytes. The tar command creates the make-3.80 directory in the working directory and unpacks the files into it.

```bash
$ ls -ld mak*
drwxrwxr-x 8 sam sam    4096 Oct  3 2002 make-3.80 
-rw-rw-r-- 1 sam sam 4823040 Jan 20 11:49 make-3.80.tar 
$ ls -l make-3.80 
total 1816 
-rw-r--r-- 1 sam sam   24687 Oct  3 2002 ABOUT-NLS 
-rw-r--r-- 1 sam sam    1554 Jul  8 2002 AUTHORS 
-rw-r--r-- 1 sam sam    18043 Dec 10 1996 COPYING 
-rw-r--r-- 1 sam sam    32922 Oct  3 2002 ChangeLog 
... 
-rw-r--r-- 1 sam sam    16520 Aug 21 2000 vmsify.c 
-rw-rw-r-- 1 sam sam    16409 Jun  9 2002 w32.c 
drwxrwxr-x 5 sam sam     4096 Oct  3 2002 w32
```

After tar extracts the files from the archive, the working directory contains two files whose names start with mak: make-3.80.tar and make-3.80. The -ld (directory) option causes ls to display only file and directory names, not the contents of directories as it normally does. The final ls command shows the files and directories in the make-3.80 directory. Refer to the tar info page for more information.

# tar: the -x option may extract a lot of files

Some tar archives contain many files. To list the files in the archive without unpacking them, run tar with the -t option and the name of the tar file. In some cases you may want to create a new directory (mkdir [page 195]), move the tar file into that directory, and expand it there. That way the unpacked files will not mingle with your existing files, and no confusion will occur. This strategy also makes it easier to delete the extracted files. Some tar files automatically create a new directory and put the files into it. Refer to the preceding example.

# tar: the -x option can overwrite files

The -x option to tar overwrites a file that has the same filename as a file you are extracting. Follow the suggestion in the preceding caution box to avoid overwriting files.
