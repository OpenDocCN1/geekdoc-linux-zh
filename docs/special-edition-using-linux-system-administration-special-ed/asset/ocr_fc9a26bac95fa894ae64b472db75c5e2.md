+   - `-L --license`—Display the gzip license and quit.
+   - `-n --no-name`—When compressing, do not save the original filename and time stamp by default. (The original name is always saved if the name had to be truncated.) When decompressing, do not restore the original filename if present (remove only the gzip suffix from the compressed filename) and do not restore the original time stamp if present (copy it from the compressed file). This option is the default when decompressing.
+   - `-N --name`—When compressing, always save the original filename and time stamp; this is the default. When decompressing, restore the original filename and time stamp if present. This option is useful on systems which have a limit on filename length or when the time stamp has been lost after a file transfer.
+   - `-q --quiet`—Suppress all warnings.
+   - `-r --recursive`—Travel the directory structure recursively. If any of the filenames specified on the command line are directories, gzip will descend into the directory and compress all the files it finds there (or decompress them in the case of gunzip).
+   - `-S .suf --suffix .suf`—Use suffix `.suf` instead of `.gz`. Any suffix can be given, but suffixes other than `.z` and `.gz` should not be used to avoid confusion when files are transferred to other systems. A null suffix forces gunzip to try decompression on all given files regardless of suffix, as in:
+     `gunzip -S "" *` (`*.*` for MSDOS). Previous versions of gzip used the `.z` suffix. This was changed to avoid a conflict with pack(1).
+   - `-t --test`—Test. Check the compressed file integrity.
+   - `-v --verbose`—Verbose. Display the name and percentage reduction for each file compressed or decompressed.
+   - `-V --version`—Version. Display the version number and compilation options then quit.
+   - `-# --fast --best`—Regulate the speed of compression using the specified digit #, where `-1` or `--fast` indicates the fastest compression method (less compression) and `-9` or `--best` indicates the slowest compression method (best compression). The default compression level is `-6` (that is, biased towards high compression at the expense of speed).

# ADVANCED USE

Multiple compressed files can be concatenated. In this case, gunzip will extract all members at once. For example:

```
gzip -c file1 > foo.gz
gzip -c file2 >> foo.gz
```