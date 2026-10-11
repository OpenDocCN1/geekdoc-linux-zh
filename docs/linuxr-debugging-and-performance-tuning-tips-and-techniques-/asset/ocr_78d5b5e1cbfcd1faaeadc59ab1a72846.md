Modern systems have considerably faster disk and memory hardware than the PDP-11s of yore. They also use a technique called *demand paging* to load into memory only those parts of an executable program that are being executed. Thus, today, the sticky bit on a regular executable file serves no purpose, and indeed it has no effect.

However, in Section 1.1.2, “Directories and Filenames,” page 6, we mentioned that the sticky bit on an otherwise writable directory prevents file removal from that directory, or file renaming within it, by anyone except the file’s owner, or **root**. Here is an example:

```
$ ls -ld /tmp                    Show /tmp’s permissions
drwxrwxrwt 19 root root 4096 Oct 20 14:04 /tmp
$ cd /tmp                       Change there
$ echo this is my file > arnolds-file      Create a file
$ ls -l arnolds-file             Show its permissions
-rw-r--r- 1 arnold devel 16 Oct 20 14:14 arnolds-file
$ su - miriam                  Change to another user
Password:
$ cd /tmp                       Change to /tmp
$ rm arnolds-file              Attempt to remove file
rm: remove write-protected regular file ‘arnolds-file’? y    rm is cautious
rm: cannot remove ‘arnolds-file’: Operation not permitted  Kernel disallows removal
```

The primary purpose of this feature is exactly for directories such as `/tmp`, where multiple users wish to place their files. On the one hand, the directory needs to be world-writable so that anyone can create files in it. On the other hand, once it’s world-writable, any user can remove any other user’s files! The directory sticky bit solves this problem nicely. Use `chmod +t` to add the sticky bit to a file or directory:

```
$ mkdir mytmp                  Create directory
$ chmod a+w+t mytmp            Add all-write, sticky bits
$ ls -ld mytmp                Verify result
drwxrwxrwt 2 arnold devel 4096 Oct 20 14:23 mytmp
```

Finally, note that the directory’s owner can also remove files, even if they don’t belong to him.

# 11.6 Setting Real and Effective IDs

Things get interesting once a process has to change its UID and GID values. Setting the group set is straightforward. Changing real and effective UID and GID values around is more involved.