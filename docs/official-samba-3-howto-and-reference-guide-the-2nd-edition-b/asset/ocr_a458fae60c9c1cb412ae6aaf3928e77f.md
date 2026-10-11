For the record, in the UNIX environment the ability to delete a file is controlled by the permissions on the directory that the file is in. In other words, a user can delete a file in a directory to which that user has write access, even if that user does not own the file.

Of necessity, Samba is subject to the file system semantics of the host operating system. Samba is therefore limited in the file system capabilities that can be made available through Windows ACLs, and therefore performs a "best fit" translation to POSIX ACLs. Some UNIX file systems do, however support, a feature known as extended attributes. Only the Windows concept of *inheriance* is implemented by Samba through the appropriate extended attribute.

The specific semantics of the extended attributes are not consistent across UNIX and UNIX-like systems such as Linux. For example, it is possible on some implementations of the extended attributes to set a flag that prevents the directory or file from being deleted. The extended attribute that may achieve this is called the *immutable* bit. Unfortunately, the implementation of the immutable flag is NOT consistent with published documentation. For example, the man page for the `chattr` on SUSE Linux 9.2 says:

> A file with the i attribute cannot be modified: it cannot be deleted or renamed, no link can be created to this file and no data can be written to the file. Only the superuser or a process possessing the `CAP_LINUX_IMMUTABLE` capability can set or clear this attribute.

A simple test can be done to check if the immutable flag is supported on files in the file system of the Samba host server.

# TEST FOR FILE IMMUTABILITY SUPPORT

+   1. Create a file called `filename`.

+   2. Login as the *root* user, then set the immutable flag on a test file as follows:

```
`root# chattr +i 'filename'`

```

+   3. Login as the user who owns the file (not *root*) and attempt to remove the file as follows:

```
`mystic:/home/hannibal > rm filename`

```

It will not be possible to delete the file if the immutable flag is correctly honored.

On operating systems and file system types that support the immutable bit, it is possible to create directories that cannot be deleted. Check the man page on your particular host system to determine whether or not immutable directories are writable. If they are not, then the entire directory and its contents will effectively be protected from writing (file creation also) and deletion.