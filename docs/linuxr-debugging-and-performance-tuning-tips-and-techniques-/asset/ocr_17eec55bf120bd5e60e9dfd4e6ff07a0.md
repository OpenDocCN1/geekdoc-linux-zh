# 5.4 Obtaining Information about Files

$ S \_ ISLNK(stbuf.st \_mode)$

Returns true if *filename* is a symbolic link. (This can never return true if $stat()$ or $fstat()$ were used instead of $lstat().$)

$ S \_ ISSOCK(stbuf.st \_mode)$

Returns true if *filename* is a socket.

> NOTE It happens that on GNU/Linux, these macros return 1 for true and 0 for false. However, on other systems, it’s possible that they return an arbitrary nonzero value for true, instead of 1. (POSIX specifies only nonzero vs. zero.) Thus, you should always use these macros as standalone tests instead of testing the return value:
> 
> if (S_ISREG (stbuf.st_mode)) ... Correct
> 
> if (S_ISREG (stbuf.st_mode) == 1) ... Incorrect

Along with the macros, <sys/stat.h> provides two sets of bitmasks. One set is for testing permission, and the other set is for testing the type of a file. We saw the permission masks in Section 4.6, “Creating Files,” page 106, when we discussed the mode_t type and values for open() and creat(). The bitmasks, their values for GNU/Linux, and their meanings are described in Table 5.2.

Several of these masks serve to isolate the different sets of bits encoded in the st_mode field:

+   - $ S \_ IFMT$ represents bits 12–15, which are where the different types of files are encoded.
+   - $ S \_ IRWXU$ represents bits 6–8, which are the user’s permission (read, write, execute for User).
+   - $ S \_ IRWXG$ represents bits 3–5, which are the group’s permission (read, write, execute for Group).
+   - $ S \_ IRWXO$ represents bits 0–2, which are the “other” permission (read, write, execute for Other).

The permission and file type bits are depicted graphically in Figure 5.3.