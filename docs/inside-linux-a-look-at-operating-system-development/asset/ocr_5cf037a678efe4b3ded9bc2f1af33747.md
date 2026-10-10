Although Multics has not inherited the full utility of security rings as used by Multics, they are mentioned here because they, along with an elaborate procedure-calling mechanism, were used to provide both great power and great security to the system.

This led naturally to a layered model of an operating system, which in turn led to the natural conclusion that the interactive user’s access to the system kernel did not have to be integral to the system kernel.

# 2.1.2 Shell

Up to this time, installing a new command line interpreter was a difficult venture. With Multics, a system administrator, or even the user, could specify how terminal interaction was to be interpreted because command interpretation was performed by a separate program—called the shell.

# 2.1.3 File System

Files on the Multics system were accessed via high-level operations that concealed the block structure of the disk. The user simply invoked an operation (read/write/etc.) with a file handle, buffer, and byte count as arguments.

Files were organized by a tree-like structure of directories, subdirectories and ultimately, files.

File data were uninterpreted by the system kernel. Although the applications could apply any interpretation desired (records, numbers, etc.), the system kernel only manipulated streams of bytes.

As a natural side effect, text files were treated as a stream of characters with a single end-of-line character separating lines. As a result, user programs could rely on easy access to data.

# 2.1.4 Dynamic Libraries

Most programs rely on collections of support subroutines held in special files called libraries. These libraries permit the programmer to reuse code others have written to parse a command line, sort an array of data,