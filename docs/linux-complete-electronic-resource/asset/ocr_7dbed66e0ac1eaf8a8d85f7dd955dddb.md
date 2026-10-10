-r --recursive Travel the directory structure recursively. If any of the file names specified on the command line are directories, gzip will descend into the directory and compress all the files it finds there (or decompress them in the case of gunzip).

-S.suf --suffix.suf Use suffix .suf instead of .gz. Any suffix can be given, but suffixes other than .z and .gz should be avoided to avoid confusion when files are transferred to other systems. A null suffix forces gunzip to try decompression on all given files regardless of suffix, as in

```
gunzip -S "" * (*.* for MSDOS)
```

Previous versions of gzip used the .z suffix. This was changed to avoid a conflict with pack(1).

-t --test Check the compressed file integrity.

-v --verbose Display the name and percentage reduction for each file compressed or decompressed.

-V --version Display the version number and compilation options then quit.

-# --fast --best Regulate the speed of compression using the specified digit #, where -1 or --fast indicates the fastest compression method (less compression) and -9 or --best indicates the slowest compression method (best compression). The default compression level is -6 (that is, biased towards high compression at expense of speed).

# ADVANCED USAGE

Multiple compressed files can be concatenated. In this case, gunzip will extract all members at once. For example:

```
gzip -c file1 > foo.gz

gzip -c file2 >> foo.gz
```

Then

```
gunzip -c foo
```

is equivalent to

```
cat file1 file2
```