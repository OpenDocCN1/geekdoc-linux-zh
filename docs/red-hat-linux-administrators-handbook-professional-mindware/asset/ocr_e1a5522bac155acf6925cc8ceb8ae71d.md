# uuencode

**Syntax:** uuencode _in_file target_name_

The uuencode command translates a binary file into readable form, by converting the binary file into ASCII printable characters. One of the many uses of uuencode is to transmit a binary file through e-mail. A file that has been uuencoded appears as a large e-mail message. The recipient can then save the message and use the uuencode command to retrieve its binary form.

The _target_name_ is the name of the binary file created when the uuencode utility is used.

The following example will uuencode the executable program `a.out`. The target name that uuencode creates will be called `b.out`. The uuencoded version of `a.out` will be saved in the file `a.out.txt`.

```
uuencode a.out b.out > a.out.txt
```

# zip

**Syntax:** zip [_-ACDe9_] _file(s)_

This compression utility compresses files in a PKZIP-compatible format, enabling compatibility with systems such as VMS, MS-DOS, OS/2, Windows NT, Minix, Atari, Macintosh, Amiga, and Acorn RISC OS.

The zip command has an array of options that are toggled by its switches. This command can create self-extracting files, add comments to zip files, remove files from an archive, and password-protect the archive.

These are a few of the features supported by zip. For a more detailed description, see your local man page.

# File System-Specific Commands

The commands in this section are used for administration of file systems.

# dd

**Syntax:** dd _if=input file_ [_conv=conversion type_ _of=output file_ [_obs=output block size_]]