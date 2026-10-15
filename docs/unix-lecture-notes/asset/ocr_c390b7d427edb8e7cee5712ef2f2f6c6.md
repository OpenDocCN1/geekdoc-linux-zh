+   - It still will not correctly display the files in directories specified on the command-line unless they are within the current working directory.
+   - The program does not print the total lines printed.
+   - It does not sort by filename.
+   - It displays all entries, including . and ..
+   - It does not display information about the three special bits of the file.

The most serious of these problems is that this version will fail if the directory argument is not in the current working directory. For example, if this is called as follows:

```
$ ls2 /
```

passing it the root directory, and there are subdirectories /etc, /usr, and /bin, the stat() function will be given the filenames "etc", "usr", and "bin". It will treat these as if they are in the current working directory since it has no way of knowing their absolute pathnames. It will fail to find them in the current working directory and will thus fail. The solution is to pass lstat() the absolute pathnames of these directories, or their correct relative names. This is accomplished by passing lstat(), for example, "/etc" instead. This implies that we need to concatenate the path of the directory argument to its file names. We could also change the working directory each time we need to list its contents, saving the old one to return to afterwards.

# 3.11 The Three Special Bits

A file's i-node and the st_mode member of the stat structure returned by the various stat() calls, each use 16 bits to define the file's permissions and type. We have accounted for a 4-bit type and 9 bits of permissions. That leaves three unexplained bits. The three bits are the set-user-id bit (setuid bit), the set-group-id bit (setgid bit) and the save-text-image bit (the sticky bit).

# 3.11.1 The Set-User-ID Bit

The setuid bit plays a critical role in UNIX. Consider the problem of allowing users to change their own passwords. A user should be able to change her password, but no one else should be able to do so, except the super-user. Since all passwords are stored in a single file, the user has to have permission to modify the password file. This implies that the user needs write permission on the password file. But if the user has write permission on the password file, then she can modify anyone else's password too, which is not acceptable. So users cannot have write permission on the password file; the file should be owned by root, and no user except the superuser should have write permission to the file. So we are back where we started, right?

Not exactly. To change a password, a user runs the passwd command. The passwd command accesses the password file and changes it. Ordinarily, when a user runs a command, the process executing the command has the same effective user-id as the user who invoked the command from the shell, and the permissions associated with that effective user-id. If this were true for the passwd