
the compressed version of the file has been replaced with the original, again with the permissions and time stamp preserved.

gzip has many options. Here are a few:

Table 19-1: gzip Options

| Option | Description |
| --- | --- |
| -c | Write output to standard output and keep original files. May also be specified with --stdout and --to-stdout. |
| -d | Decompress. This causes gzip to act like gunzip. May also be specified with --decompress or --uncompress. |
| -f | Force compression even if compressed version of the original file already exists. May also be specified with --force. |
| -h | Display usage information. May also be specified with --help. |
| -l | List compression statistics for each file compressed. May also be specified with --list. |
| -r | If one or more arguments on the command line are directories, recursively compress files contained within them. May also be specified with --recursive. |
| -t | Test the integrity of a compressed file. May also be specified with --test. |
| -v | Display verbose messages while compressing. May also be specified with --verbose. |
| -number | Set amount of compression. number is an integer in the range of 1 (fastest, least compression) to 9 (slowest, most compression). The values 1 and 9 may also be expressed as --fast and --best, respectively. The default value is 6. |

Going back to our earlier example:

```
[me@linuxbox ~]$ gzip foo.txt
[me@linuxbox ~]$ gzip -tv foo.txt.gz
foo.txt.gz: OK
[me@linuxbox ~]$ gzip -d foo.txt.gz
```

Here, we replaced the file foo.txt with a compressed version, named foo.txt.gz.

Next, we tested the integrity of the compressed version, using the -t and -v options. Finally, we decompressed the file back to its original form.

gzip can also be used in interesting ways via standard input and output:

```
[me@linuxbox ~]$ ls -l /etc | gzip > foo.txt.gz
```

This command creates a compressed version of a directory listing.

The gunzip program, which uncompresses gzip files, assumes that filenames end in the extension .gz, so it's not necessary to specify it, as long as the specified name is not in conflict with an existing uncompressed file:

```
[me@linuxbox ~]$ gunzip foo.txt
```

If our goal were only to view the contents of a compressed text file, we can do this:

```
[me@linuxbox ~]$ gunzip -c foo.txt | less
```

Alternately, there is a program supplied with gzip, called zcat, that is equivalent to gunzip with the -c option. It can be used like the cat command on gzip compressed files:

```
[me@linuxbox ~]$ zcat foo.txt.gz | less
```

> Tip: There is a zless program, too. It performs the same function as the pipeline above.

## bzip2

The bzip2 program, by Julian Seward, is similar to gzip, but uses a different compression algorithm that achieves higher levels of compression at the cost of compression speed. In most regards, it works in the same fashion as gzip. A file compressed with bzip2 is denoted with the extension .bz2:

```
[me@linuxbox ~]$ ls -l /etc > foo.txt
[me@linuxbox ~]$ ls -l foo.txt
-rw-r--r-- 1 me me 15738 2008-10-17 13:51 foo.txt
[me@linuxbox ~]$ bzip2 foo.txt
[me@linuxbox ~]$ ls -l foo.txt.bz2
-rw-r--r-- 1 me me 2792 2008-10-17 13:51 foo.txt.bz2
[me@linuxbox ~]$ bunzip2 foo.txt.bz2
```

As we can see, bzip2 can be used the same way as gzip. All the options (except for -r) that we discussed for gzip are also supported in bzip2. Note, however, that the compression level option (-number) has a somewhat different meaning to bzip2. bzip2 comes with bunzip2 and bzcat for decompressing files.

bzip2 also comes with the bzip2recover program, which will try to recover damaged .bz2 files.

## Don't Be Compressive Compulsive

I occasionally see people attempting to compress a file, which has been already compressed with an effective compression algorithm, by doing something like this:

```
$ gzip picture.jpg
```

Don't do it. You're probably just wasting time and space! If you apply compression to a file that is already compressed, you will actually end up a larger file. This is because all compression techniques involve some overhead that is added to the file to describe the compression. If you try to compress a file that already contains no redundant information, the compression will not result in any savings to offset the additional overhead.

## Archiving Files

A common file management task used in conjunction with compression is archiving. Archiving is the process of gathering up many files and bundling them together into a single large file. Archiving is often done as a part of system backups. It is also used when old data is moved from a system to some type of long-term storage.

## tar

In the Unix-like world of software, the tar program is the classic tool for archiving files.
