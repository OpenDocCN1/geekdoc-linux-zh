The `ls` listing in Figure 6.1 shows the following information, from left to right:

+   - The character in the first column reflects the file type and can be one of the following:
+     - `-`, as shown in the example, means this is a regular file.
+     - `b` is a block (buffered) special file (such as a tape drive or floppy drive—for example, `/dev/fd0`).
+     - `c` or `u` is a character-oriented (unbuffered) special file (such as a terminal device—for example, `/dev/ttyp0`).
+     - `d` means it’s a directory.
+     - `l` is for a symbolic link.
+     - `p` is a special FIFO (first in, first out) file (such as a named pipe).
+     - `s` is a socket file that provides interprocess networking.

+   - The first triplet of permission settings (`rw-`) indicates the file owner can read and write to the file but not execute it (as a binary program or a shell script).
+   - The second triplet (`r--`) indicates the members of the file’s group can only read the file.
+   - The third triplet (`r--`) indicates everyone else (often referred to as world, as in “rest of the world”) can only read the file.

# NOTE

If a `+` is displayed after the others’ permissions (such as `r--+`), it means an access control list (ACL) is assigned to the file. See the “Extended File Attributes” section later in this chapter for details.

+   - The number of (hard) links to the file; only one link in this example.
+   - The file owner is user root.
+   - The file group owner is the root group.
+   - File size in bytes (13 bytes in this case).
+   - The modification time.
+   - Name of the file, `myFile`.

# NOTE

For a shell to execute a file containing shell script commands, the file must have the proper `x` permission bits set. For instance, for both the file and group owners to be able to run the script file, the `x` permission must be set on the