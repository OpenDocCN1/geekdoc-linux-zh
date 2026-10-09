The permission bits that end up in a newly created file are formed by ANDing the ones in the system call with the complement of process's file mode creation mask, typically set at login time (with the `umask` command), or with the `umask` system call (Section 2.5). The “ANDing the complement” business just means that if a bit is set in the mask, it's cleared in the permissions. Thus, a mask of 002 would cause the $S_{-}IWOTH$ bit (write permission for others) to be cleared, even if the flag $S_{-}IWOTH$ appeared in the call to open. As a programmer, however, you don't usually think about the mask, since it's something users do to *restrict* permissions.

What if you create a file with the O_WRONLY or O_RDWR flags but the permission bits don't allow writing? As the file is brand new, it is *still* opened for writing. However, the next time it's opened it will already exist, so then the permission bits will control access as described in the previous section.

Sometimes you always want a *fresh* file, with no data in it. That is, if the file exists you want its data to be thrown away, with the file offset set at zero. The O_TRUNC flag does that:

```
```
c_e_neg1( fd = open("/home/marc/newFile", O_WRONLY | O_CREAT | O_TRUNC,
PERM_FILE) )
```
```

Since O_TRUNC destroys the data, it's allowed on an existing file only if the process has write permission, as it is a form of writing. Similarly, it can't be used if the O_RDONLY flag is also set.

For a *new* file (i.e., O_CREAT doing its thing), you need write permission in the parent directory, since a new link would be added to it. For an *existing* file, the permissions on the directory don't matter; it's the file's permissions that count. The way to think of this is to ask yourself, “What needs to be written to complete this operation?”

I might also mention that you need search (execute) permission on the intermediate directories in the path (i.e., home and marc). That, however, universally applies to any use of a path, and we won't say it every time.

O_TRUNC doesn't have to be used with O_CREAT. By itself it means “truncate the file to zero if it exists, and just fail if it doesn't exist.” (Maybe there's a logging feature that gets turned on by creating a log file; no log file means no logging.)

The combination O_WRONLY | O_CREAT | O_TRUNC is so common (“create or truncate a file for writing”) that there's a special system call just for it: