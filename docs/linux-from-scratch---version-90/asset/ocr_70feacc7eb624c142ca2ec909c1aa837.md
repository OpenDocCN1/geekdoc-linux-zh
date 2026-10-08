# 6.62. Gzip-1.10

The Gzip package contains programs for compressing and decompressing files.

Approximate build time: 0.1 SBU
Required disk space: 20 MB

# 6.62.1. Installation of Gzip

Prepare Gzip for compilation:

```
./configure --prefix=/usr
```

Compile the package:

```
make
```

To test the results, issue:

```
make check
```

Two tests are known to fail in the LFS environment: help-version and zmore.

Install the package:

```
make install
```

Move a program that needs to be on the root filesystem:

```
mv -v /usr/bin/gzip /bin
```

# 6.62.2. Contents of Gzip

Installed programs:
gunzip, gzexe, gzip, uncompress (hard link with gunzip), zcat, zcmp, zegrep, zdiff, zfgrep, zforce, zgrep, zmore, and znew

# Short Descriptions

+   - gunzip Decompresses zipped files
gzexe Creates self-decompressing executable files
gzip Compresses the given files using Lempel-Ziv (LZ77)
uncompress Decompresses compressed files
zcat Decompresses the given zipped files to standard output
zcmp Runs cmp on gzipped files
zdiff Runs diff on gzipped files
zegrep Runs egrep on gzipped files
zfgrep Runs grep on gzipped files
zforce Forces a .gz extension on all given files that are gzipped files, so that gzip will not compress again; this can be useful when file names were truncated during a file transfer
zgrep Runs grep on gzipped files