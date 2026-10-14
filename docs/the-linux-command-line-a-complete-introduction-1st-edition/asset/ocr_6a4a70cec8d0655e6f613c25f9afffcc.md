Let’s look again at our earlier example:

```
[me@linuxbox ~]$ gzip foo.txt
[me@linuxbox ~]$ gzip -tv foo.txt.gz
foo.txt.gz:         OK
[me@linuxbox ~]$ gzip -d foo.txt.gz
```

Here, we replaced the file foo.txt with a compressed version named foo.txt.gz. Next, we tested the integrity of the compressed version, using the -t and -v options. Finally, we decompressed the file back to its original form. gzip can also be used in interesting ways via standard input and output:

```
[me@linuxbox ~]$ ls -l /etc | gzip > foo.txt.gz
```

This command creates a compressed version of a directory listing. The gunzip program, which uncompresses gzip files, assumes that filenames end in the extension .gz, so it’s not necessary to specify it, as long as the specified name is not in conflict with an existing uncompressed file:

```
[me@linuxbox ~]$ gunzip foo.txt
```

If our goal were only to view the contents of a compressed text file, we could do this:

```
[me@linuxbox ~]$ gunzip -c foo.txt | less
```

Alternatively, a program supplied with gzip, called zcat, is equivalent to gunzip with the -c option. It can be used like the cat command on gzip-compressed files:

```
[me@linuxbox ~]$ zcat foo.txt.gz | less
```

Note: There is a zless program, too. It performs the same function as the pipeline above.

# bzip2—Higher Compression at the Cost of Speed

The bzip2 program, by Julian Seward, is similar to gzip but uses a different compression algorithm, which achieves higher levels of compression at the cost of compression speed. In most regards, it works in the same fashion as gzip. A file compressed with bzip2 is denoted with the extension .bz2:

```
[me@linuxbox ~]$ ls -l /etc > foo.txt
[me@linuxbox ~]$ ls -l foo.txt
-rw-r--r-- 1 me me 15738 2012-10-17 13:51 foo.txt
[me@linuxbox ~]$ bzip2 foo.txt
[me@linuxbox ~]$ ls -l foo.txt.bz2
-rw-r--r-- 1 me me 2792 2012-10-17 13:51 foo.txt.bz2
[me@linuxbox ~]$ bunzip2 foo.txt.bz2
```