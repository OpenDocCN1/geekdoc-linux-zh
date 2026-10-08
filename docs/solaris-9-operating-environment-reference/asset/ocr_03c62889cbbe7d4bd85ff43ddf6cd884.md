# tar 1379

argument. In the case where you also specify included files (see the
-I include-file option), the excluded files take precedence over all
included files. If you specify a file in both the exclude-file and the
include-file(or on the command line), tar excludes it.

@ Include extended attributes in archive. By default, tar does not put
extended attributes in the archive. With this flag, tar allows for
extended attributes on the files to be put in the archive and adds them
to the archive. Extended attributes go into the archive as special files
with a special label. When you use this modifier with the x
function, extended attributes are extracted from the tape along with
normal file data. You can extract extended attributes only as
part of a normal file extract. Attempts to explicitly extract attribute
records are ignored. Extended attributes are new in the Solaris 9
release.

[0-7] Select an alternative drive on which the tape is mounted. The default
entries are specified in /etc/default/tar. If you specify no drive or f
function modifier, the default is the entry in /etc/default/tar with
drive 0.

# Usage

See larg(5) for the description of the behavior of tar when encountering files
gr than or equal to 2 Gbytes (2**31 bytes).
The automatic detection of the actual blocking factor can be fooled by a pipe
or a socket (see the B function modifier) is read.
Quarter-inch streaming tape has an inherent blocking factor of 512-byte block.
You can read or write to it with any blocking factor.
The B function modifier works for archives on disk files and block special devices,\among others, but it is intended principally for tape devices.
For information on tar header format, see archives(4).

# Examples

The following example uses tar to create an archive of your home directory on a tape
mounted on drive /dev/rmt/

```
castle% cd
castle% cvf /dev/rmt/0 .
messages from tar
```

The function letter creates the archive; the v modifier outputs messages
explaining what tar is doing; the f modifier indicates the specified tarfile
(/dev/rmt/0 in this example). The dot (.) at the end of the command line means the
current directory and is the argument of the f modifier.

The following example displays the table of contents of the tarfile. The output for the
POSIX locale is shown.

```
castle% tar tvf /dev/rmt/0
rw-r--r-- 1677/40 2123 Mar  7 18:15:1999      ./test.c...
castle%
```