mainly because of zip's compatibility with Phil Katz's PKZIP program. Files compressed with zip have the .zip extension.

The zip command has an array of options that are toggled by its switches. This command can create self-extracting files, add comments to ZIP files, remove files from an archive, and password-protect the archive.

These are a few of the features zip supports. For a more detailed description, see your local zip man page.

# File Systems – Specific Commands

The commands that I discuss in this section deal with file systems. Using these commands you can create and format file systems, check disk usage, and so on.

# dd

Syntax: dd if=input file [conv=conversion type] of=output file [obs=output block size]

This program allows you to convert ASCII and EBCDIC (IBM) file formats. For example:

```
dd if=/tmp/uppercase.txt  conv=lcase of=/tmp/lowercase.txt
```

This command takes the /tmp/upppercase.txt file and writes a new file called /tmp/lowercase.txt and converts all characters to lowercase (lcase). To do the reverse, you can use conv=ucase option. However, dd is most widely used to write a boot image file to a floppy disk that has a file system that mkfs has already created. For example:

```
dd if=/some/boot.img  conv=lcase of=/dev/fd0 obs=16k
```

This command writes the /some/boot.image file to the first floppy disk (/dev/fd0) in 16K blocks.

# df

Syntax: df [-k] FileSystem | File