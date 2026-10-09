
In short, what you are doing here is creating an archive, listing that archive (with `-t`), extracting the `fl` file, and then extracting all of the files.

## Task 6

Another useful command for backups is `dd`. Typically this is used for block-level copying of an entire disk or partition, but it can also be used with ordinary files:

```
dd if=f1 of=f1.bak
```

Of course, if that's all you were doing, you could just use `cp`. A more typical usage would be something like (do not actually run this):

```
dd if=/dev/sda1 of=/dev/sdb1
```

Assuming you had already connected a backup drive, this would copy the entire `/dev/sda1` partition onto it.

## Task 7

Finally, clean up:

```
cd ~
rm -r lab45
```

## Notes

To use compression-only without `tar` for archiving, each format has its own compression and decompression commands. Use `gzip/gunzip`, `bzip2/bunzip2`, and `xz/unxz`, for `gzip`, `bzip2`, and `LZMA` formats, respectively.
