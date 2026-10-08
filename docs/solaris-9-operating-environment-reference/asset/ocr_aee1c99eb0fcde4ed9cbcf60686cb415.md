# 482 gzip, gunzip, zcat

-L --license

Display the gzip license, and quit.

-n --no-name

When compressing, do not save the original file name and timestamp by default. (The original name is always saved if the name was truncated). Whening, do not restore the original file name if present (remove only the gzip suffix from the compressed file name) and do not restore the original timestamp if present (copy it from the compressed file). This option is the default when decompressing.

-N --name

When compressing, always save the original file name and timestamp (the default). When decompressing, restore the original file name and timestamp if present. This option is useful on systems that have a limit on file-name length or when the timestamp has been lost after a file transfer.

-q --quiet Suppose all warnings.

-r --recursive

Travel the directory structure recursively. If any of the file names specified on the command line are directories, gzip descends into the directory and compresses all the files it finds (or decompresses in the case of gzip).

-s --suffix .suffix

Use suffix .suffix instead of .gz. You can specify any suffix, but you should avoid others other than .z and .gz to prevent confusion when files are transferred to other systems. A null suffix forces gzip to try decompression on all given files regardless of suffix, as shown in the example below

```
gzip -s ".*" for MS-DOS
```

Previous versions of gzip used the .z suffix. This suffix was changed to avoid a conflict with pack(1).

-t --test Check the compressed file integrity.

-v --verbose

Verbose. Display the name and percentage reduction for each file compressed or decompressed.

-V --version

Version. Display the version number and compilation options, then quit.

# --fast --best

Regulate the speed of compression with the specified digit #, -1 or --fast indicates the fastest compression method (less compression) and -9 or --best indicates the slowest compression method (best). The default compression level is -6 (that is, biased toward high compression at the expense of speed).