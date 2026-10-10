```
[ -I, --one-file-system ] [ -L, --tape-length N ]
[ -m, --modification-time ] [ -M, --multi-volume ]
[ -N, --after-date DATE, --newer DATE ]
[ -o, --old-archive, --portability ] [-O, --to-stdout ]
[ -p, --same-permissions, --preserve-permissions ]
[ -P, --absolute-paths ] [ --preserve ] [ -R, --record-number ]
[ --remove-files ] [ -s, --same-order, --preserve-order ]
[ --same-owner ] [ -S, --sparse ] [ -T, --files-from F ] [ --null ]
[ --totals ] [ -v, --verbose ] [ -V, --label NAME ] [ --version ]
[ -w, --interactive, --confirmation ] [ -W, --verify ] [ --exclude FILE ]
[ -X, --exclude-from FILE ] [ -Z, --compress, --uncompress ]
[ -z, --gzip, --ungzip ] [ --use-compress-program PROG ]
[ --blockcompress ] [ [-0-7] ] [ mbh ]

filename1 [ filename2, ... filenameN ]
directory1 [ directory2, ... directoryN ]
```

# DESCRIPTION

This manual page documents the GNU version of tar , an archiving program designed to store and extract files from an archive file known as a tarfile. A tarfile may be made on a tape drive, however, it is also common to write a tarfile to a normal file. The first argument to tar must be one of the options: A c d r u , followed by any optional functions. The final arguments to tar are the names of the files or directories which should be archived. The use of a directory name always implies that the subdirectories below should be included in the archive.

# FUNCTION LETTERS

One of the following options must be used:

+   - -A, --catenate, --concatenate Append tar files to an archive.
+   - -c, --create Create a new archive.
+   - -d, --diff, --compare Find differences between archive and file system.
+   - -delete Delete from the archive (not for use on mag tapes!).
+   - -r, --append Append files to the end of an archive.
+   - -t, --list List the contents of an archive.