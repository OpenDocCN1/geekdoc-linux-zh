# zip

Syntax:

```
zip [-ACde9] file(s)
```

This compression utility compresses files in a PKZIP compatible format, enabling compatibility with systems such as VMS, MS-DOS, OS/2, Windows NT, Minix, Atari, Macintosh, Amiga, and Acorn RISC OS.

The zip command has an array of options that are toggled by its switches. This command can create self-extracting files, add comments to zip files, remove files from an archive, and password-protect the archive.

These are a few of the features supported by zip. For a more detailed description, see your local man page.

# File System-Specific Commands

The commands in this section are used for administration of file systems.

# dd

Syntax:

```
dd if=input file [conv=conversion type] of=output file [obs=output block size]
```

This program allows you to convert file formats. For example,

```
dd if=/tmp/uppercase.txt conv=lcase of=/tmp/lowercase.txt
```

takes the /tmp/uppercase.txt file and writes a new file called /tmp/lowercase.txt, converting all the characters to lowercase (lcase). To do the reverse, you can use conv=ucase option. However, dd is most widely used to write a boot image file to a floppy disk that has a file system already created by mkfs. For example,

```
dd if=/some/boot.img conv=lcase of=/dev/fd0 obs=16k
```

writes the /some/boot.image file to the first floppy disk (/dev/fd0) in 16K blocks.