# Advanced Bash–Scripting Guide

+   3. -r append (files to the archive)
4. -t list (archive contents)
5. -u update archive
6. -x extract (files from the archive)
7. -z gzip the archive

It may be difficult to recover data from a corrupted gzipped tar archive. When archiving files, make multiple backups.

shar

Shell archiving utility. The files in a shell archive are concatenated without compression, and the resultant archiving is essentially a shell script, complete with #!/bin/sh header, and containing all the necessary unarchiving commands. Shar archives show up in Internet newsgroups, but otherwise shar has been pretty well replaced by tar/gzip. The unshar command shar archives.

ar

Creation and manipulation utility for archives, maintained widely used for binary object files.

cpio

This specialized archiving copy command (copy input and output) is rarely seen any more, having been supplanted by tar/gzip. It still has its uses, as moving a directory tree.

# Example 12–22. Using cpio to move to a directory tree

```
#!/bin/bash

# Copying a directory tree using cpio

ARGS=2
E_BADARGS=65

if [ $# -ne "$ARGS" ];
then
    echo "Usage: basename $0 destination"
    exit $E_BADARGS
fi

source=$1
destination=$2

find "$source" -depth cpio -admv "$destination"
# Read the man page to decipher these cpio options.

exit 0
```

# Example 12–23. Unpacking an rpm archive

```
#!/bin/bash
# de-rpm.sh: Unpack an 'rpm'
```

12.5. File and Archiving Commands