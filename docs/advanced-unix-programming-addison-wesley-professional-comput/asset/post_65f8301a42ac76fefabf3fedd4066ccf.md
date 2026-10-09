
$ df /usr

Filesystem 1k-blocks Used Avail Capacity Mounted on
/dev/ad0s1g 3408662 988696 2147274 32% /usr

The reported number of 1k-blocks, 3408662, equates to the number of 2k-blocks that our `print_statvfs` program showed, 1704331.

There’s also a standard way to read the information in an i-node, so you don’t have to read the device file as we did in the previous section. We’ll get to that in Section 3.5.

## 3.2.4 Mounting and Unmounting File Systems

A UNIX system can have lots of disk file systems (hard disks, floppies, CD-ROMs, DVDs, etc.), but they’re all accessible within a single directory tree that starts at the root. Connecting a file system to the existing hierarchy is called *mounting*, and disconnecting it *unmounting*. Figure 3.1 shows a large file system that contains the root (i-node 2, with directory entries x and y) and a smaller unconnected file system, with its own root, also numbered 2. (Recall that 2 is always the i-number for a root directory.)

![](img/41b4c8f6d6a5c349eee321a301703d97_149_0.png)

**Figure 3.1** Two disconnected file systems.

![](img/41b4c8f6d6a5c349eee321a301703d97_150_0.png)

**Figure 3.2** Mounted file system.

To mount the second file system, you need two things: Its device name, which is /dev/ad0slm, and the directory where you want to connect it, for which we'll choose /y/a (i-node 221). Here's the command that creates the tree in Figure 3.2:

```bash
# mount /dev/ad0slm /y/a
```

The old contents of directory /y/a are now hidden, and all references to that directory automatically become references to i-node ad0slm:2, a notation that I'll use to mean “i-node 2 on device ad0slm.” Thus, the file ad0slm:107 is now accessible as /y/a/f. When ad0slm is unmounted, its contents are no longer accessible, and the old contents of ad0s1g:221 reappear.³

Every UNIX system has a superuser-only system call named mount and its undo-function unmount (sometimes called umount), but their arguments and exact behavior vary from system to system. Like other superuser-only functions, they're not standardized. In practice, these systems calls are used to implement the mount and unmount commands and are almost never called directly. As an example, here are the Linux synopses, which I won't bother to explain completely:

```c
mount—mount file system (nonstandard)

#include <sys/mount.h>

int mount(
    const char *source,    /* device */
    const char *target,     /* directory */
    const char *type,       /* type (e.g., ext2) */
    unsigned long flags,    /* mount flags (e.g., MS_RDONLY) */
    const void *data        /* file-system-dependent data */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

```c
umount — unmount file system (nonstandard)

#include <sys/mount.h>

int umount(
    const char *target     /* directory */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

Normally, umount fails with the error EBUSY if any file or directory on it is in use. There's usually an alternative system call named umount2 that has a flag as a second argument that forces the umount, which is occasionally essential when the system has to be shut down.

From the application-programming perspective, except for one situation, you're normally not concerned with the fact that a given file or directory you're trying to access is on a file system separately mounted from some other file or directory, as long as you have a path name that works. In fact, all accessible file systems, even the root, had to be mounted at one time, perhaps during the boot sequence. The one situation has to do with links, which is what the next section is about.

³ It's rare to actually have anything in a directory whose only purpose is to serve as a mount point, but it's allowed and occasionally used by system administrators to hide a directory.

## 3.3 Hard and Symbolic Links

An entry in a directory, consisting of a name and an i-number, is called a hard link. The other kind of link is a symbolic link, which I'll talk about in a moment. Figure 3.3.3 illustrates both. (The hex numbers in parentheses are device IDs, which I'll explain later.)

![](img/41b4c8f6d6a5c349eee321a301703d97_152_0.png)

Figure 3.3 Hard and symbolic links.

### 3.3.1 Creating Hard Links ( link System Call)

You get a hard link when a file of any type, including directory, is created. You can get additional hard links to nondirectories ⁴ with the link system call:

```c
/*—create hard link
#include <unistd.h>

int link(
    const char *oldpath, /* old pathname */
    const char *newpath  /* new pathname */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

The first argument, oldpath, must be an existing link; it provides the i-number to be used. The second argument, newpath, indicates the name of the new link. The links are equal in every way, since UNIX has no notion of primary and secondary links. The process must have write permission on the directory that is to contain the new link. The link specified by the second argument must not already exist; `link` can't be used to change an existing link. In this case the old link must first be removed with `unlink` (Section 2.6), or the `rename` system call can be used (next section).

⁴ On some systems the superuser can link to an existing directory, but doing so means the directory structure is no longer a tree, complicating system administration.

### 3.3.2 Renaming a File or Directory (rename System Call)

At first thought it seems easy to rename a file, if by that you mean “change the name in the directory entry.” All you do is make a second hard link with `link` and remove the old link with `unlink`, but there are many complications:

- The file may be a directory, which you can't make a second hard link to.
- Sometimes you want the new name to be in a different directory, which is no problem if it's on the same file system, but a big problem if it isn't, because `link` only works within a file system. You can, of course, create a symbolic link (next section) in the new directory, but that's not what most people mean by “rename.”
- If it's a directory that you want to “rename” (“move,” really) between file systems, you have to move the whole subtree beneath it. Moving only empty directories is too restrictive.
- If there are multiple hard links and you're renaming the file within the same file system, they're going to be OK, because they reference the i-number, which won't change. But if you somehow manage to move the file to another file system, the old links will no longer be valid. What might happen, since you have to copy the file and then unlink the original, is that the old copy will stay around with all but the moved hard link still linked to it. Not good.
- If there are symbolic links to a path and you change that path, the symbolic links become dead ends. Also not good.

There are probably even more complications that we could list if we thought about it some more, but you get the idea, and we're already getting a headache. That's why the UNIX `mv` command, which is what you use to “rename” a file or directory, is a very complex piece of code. And it doesn't even deal with the last two problems.

Anyway, the `mv` command does pretty well, but to move a directory within a file system it needs one of the following alternative mechanisms.

- To always copy a directory and its subtree, followed by a deletion of the old directory, even if the directory is just renamed within its parent.
- A `link` system call that will work on directories, even if restricted to the superuser (The `mv` command can run with the set-user-ID bit on, to temporarily take on the privileges of the superuser.)
- A new system call that can rename a directory within a file system

The first alternative is bad—that’s way too much work if all you want to do is change a few characters in the name! The second was ruled out by POSIX in favor of the third—a new system call, `rename`. Actually, it isn’t new—it was in Standard C and had been in BSD. It’s the only way to rename a directory without a full `copy`/`unlink`.

```c
rename—rename file

#include <stdio.h>

int rename(
         const char *oldpath,         /* old pathname */
         const char *newpath          /* new pathname */
      );
/* Returns 0 on success or -1 on error (sets errno) */
```

rename is roughly equivalent to the sequence:

1.  If `newpath` exists, remove it with `unlink` or `rmdir`.
2.  `link(oldpath, newpath)`, even if `oldpath` is a directory.
3.  Remove `oldpath` with `unlink` or `rmdir`.

What `rename` brings to the table are some additional features and rules:

-   As I mentioned, step 2 works on directories, even if the process isn’t running as the superuser. (You need write permission in `newpath`’s parent, though.)
-   If `newpath` exists, it and `oldpath` have to be both files or both directories.
-   If `newpath` exists and is a directory, it has to be empty. (Same rule as for `rmdir`.) In step 3, `oldpath`, if a directory, is removed even if nonempty, since its contents are also in `newpath`.
-   If `rename` fails somewhere along the way, everything is left unchanged.

So you can see that while steps 1, 2, and 3 look like you could write them as a library function, there’s no way to get it to work like the system call.
