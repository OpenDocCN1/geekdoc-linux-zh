
| Option | Meaning |
| --- | --- |
| -c | Create an archive. |
| -f | Use the specified output filename. |
| -h | Follow symbolic links as if they were normal files or directories. |
| -H | Follow symbolic links on the command line only. |
| -j | Use bzip2 for compression. |
| -m | Do not preserve file modification times. |
| -p | Preserve user and group ID as well as file mode information. |
| -t | Show the table of contents of an archive. |
| -v | Enter verbose mode for more explanatory output. |
| -x | Extract files from an archive. |
| -Z | Compress an archive using compress. |
| -z | Compress an archive using gzip. |

## TABLE 19.1 Useful Options to tar

If you have a remote Unix account and a local PC or Macintosh, one great use of tar is to occasionally build an archival snapshot of all your files and then FTP them to your local computer. We’ll talk about this in the latter part of this hour.

## The zip Archive Utility

While tar is a popular archival utility for the Unix world—including Linux—when you get to the land of PCs and laptops, the ZIP archive format turns out to be far more common and far more popular. The good news is that there’s a command-line ZIP interface available in modern Unixes like Solaris, so let’s have a look!

## Task 19.2: Learning to Use zip

If you thought that the tar command had a lot of command flags and options, wait until you get a look at zip. It’s so complicated that just about every time I use it, I have to read the man page again to see some examples. And I’ve been working with Unix and command lines for a ridiculously long time.

Let’s take a look.

- 1. To start out, I’ll do the same thing I did in Task 19.1: Create a quick archival snapshot of all the files and folders in my home directory. But this time, I’ll create an output file in /tmp:

Click here to view code image

```
$ zip /tmp/archive *
  adding: Desktop/ (stored 0%)
  adding: Documents/ (stored 0%)
  adding: Downloads/ (stored 0%)
  adding: Public/ (stored 0%)
  adding: cmdcnt.sh (deflated 45%)
```

adding: diskspace.sh (deflated 24%)
adding: hi-low.sh (deflated 44%)
adding: test/ (stored 0%)
adding: testme (stored 0%)

- 2. Here's what I've created:

Click here to view code image

```
$ ls -l /tmp/*zip
-rw-rw-- 1 taylor staff 2016 Apr 30 15:11 /tmp/archive.zip
```

This seems quite small, but a close examination reveals that most of my directories are empty (Desktop, Documents, Downloads, etc.), which is why the zip command reported stored 0% when it encountered them.

- 3. Creating an archive is easily done with no command flags needed. But, oh, there are plenty of command flags, which you can summarize with the -h help flag:

Click here to view code image

```
$ zip -h
Copyright (c) 1990-2008 Info-ZIP - Type 'zip "-L"' for software license.
Zip 3.0 (July 5th 2008). Usage:
zip [-options] [-b path] [-t mmddyyyy] [-n suffixes] [zipfile list] [-xi list]
The default action is to add or replace zipfile entries from list, which can include the special name - to compress standard input.
If zipfile and list are omitted, zip compresses stdin to stdout.
-f freshen: only changed files -u update: only changed or new files
-d delete entries in zipfile -m move into zipfile (delete OS files)
-r recurse into directories -j junk (don't record) directory names
-0 store only -l convert LF to CR LF (-11 CR LF to LF)
-1 compress faster -9 compress better
-q quiet operation -v verbose operation/print version info
-c add one-line comments -z add zipfile comment
-@ read names from stdin -o make zipfile as old as latest entry
-x exclude the following names -i include only the following names
-F fix zipfile (-FF try harder) -D do not add directory entries
-A adjust self-extracting exe -J junk zipfile prefix (unzipsfx)
-T test zipfile integrity -X eXclude eXtra file attributes
-y store symbolic links as the link instead of the referenced file
-e encrypt -n don't compress these suffixes
-h2 show more help
```

- 4. With those flags in mind, I want to get a table of contents listing of the archival ZIP file. You can do this and also actually unpack a ZIP archive through a different command called unzip, logically enough. Without any arguments, it offers up some help information:

Click here to view code image

```
$ unzip
UnZip 6.00 of 20 April 2009, by Info-ZIP. Maintained by C. Spieler.
Sendbug reports using http://info-zip.org/zip-bug.html; see README for details.

Usage: unzip [-Z] [-opts[modifiers]] file[.zip] [list] [-x xlist] [-d
```
