# zip, zipplok, zipnote, zipsplit 1581

tar cf - | zip backup -

This command generally produces better compression than the previous example with the -r option because zip can take advantage of redundancy between files. You can restore the backup with the following command.

```
unzip -p backup | tar xf -
```

When you specify no zipfilename and standard output is not a terminal, zip acts as a filter, compressing standard input to standard output. The following example

```
tar cf - | zip | dd of=/dev/nrst0 obs=16k
```

is equivalent to

```
tar cf - | zip - | dd of=/dev/nrst0 obs=16k
```

You can extract zip archives that are created in this way with the funzip command, which is provided in the unzip package or by gunzip, which is provided in the gzip package. The following example shows the syntax for extracting a zip archive with funzip.

```
dd if=/dev/nrst0 bs=16k | funzip | tar xvf
```

When changing an existing zip archive, zip writes a temporary file with the new contents and replaces the old one only when the process of creating the new version has been completed without error.

If the name of the zip archive does not contain an extension, the extension .zip is added. If the name already contains an extension .zip, the existing extension is unchanged.

# Options

+   -a [Systems with EBCDIC] Translate file to ASCII format.
-A Adjust self-extracting executable archive. Create a self-extracting executable archive by prepending the SFX stub to an existing archive. The -A option tells zip to adjust the entry offsets stored in the archive to take into account this "preamble" data.
Note: Self-extracting archives for the Amiga are a special case. When present, the Amiga port of zip is capable of adjusting or updating archives without corrupting them. You can use the -J option to remove the SFX stub if you need to make updates.
-b path Use the specified path for the temporary zip archive. The following example puts the temporary zip archive in the directory /tmp, copying stuff.zip to the current directory when done.\zip -b /tmp * This option is only useful when updating an existing archive and the file system containing the old archive does not have enough space to hold both old and new archives at the same time.
-B /CMS and MVS/ Force file to be read as binary (default is text).