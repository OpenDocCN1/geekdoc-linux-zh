
## Real World Scenario
### Backing Up Using Optical Media

Optical media require special backup procedures. Normally, cdrecord accepts input from a program like mkisofs, which creates an ISO-9660 or UDF file system—the type of file system that’s most often found on CD-ROMs and DVDs.

One option for backing up to optical discs is to use mkisofs and then cdrecord to copy files to the disc. If you copy files “raw” this way, though, you’ll lose some information, such as write permission bits. You’ll have better luck if you create a tar or cpio archive on disk. You can then use mkisofs to place that archive in an ISO-9660 or UDF file system, and then burn the image file to the optical disc. The result will be a disc that you can mount and that will contain an archive you can read with tar or cpio.

A somewhat more direct option is to create an archive file and burn it directly to the optical disc using cdrecord, bypassing mkisofs. Such a disc won’t be mountable in the usual way, but you can access the archive directly by using the CD-ROM device file. On restoration, this works much like a tape restore except that you specify the optical device filename (such as /dev/cdrom) instead of the tape device filename (such as /dev/st0).

## Managing Links

In Linux, a link is a way to give a file multiple identities, similar to shortcuts in Windows and aliases in Mac OS. Linux employs links to help make files more accessible, to give commands multiple names, to enable programs that look for the same file in different locations to access the same files, and so on. Two types of links exist: hard links and soft links (a.k.a. symbolic links). (Their differences are described in more detail shortly.) The ln command creates links. Its syntax is similar to that of cp:

```
ln [options] source link
```

The source is the original file, and the link is the name of the link you want to create. This command supports options that have several effects:

- **Remove target files**: The -f or --force option causes ln to remove any existing links or files that have the target link name. The -i or --interactive option has a similar effect, but it queries you before replacing existing files and links.
- **Create directory hard links**: Ordinarily, you can’t create hard links to directories. The root user can attempt to do so, though, by passing the -d, -F, or --directory option to ln. (Symbolic links to directories aren’t a problem.) In practice, this feature is unlikely to work because most file systems don’t support it.
- **Create a symbolic link**: The `ln` command creates hard links by default. To create a symbolic link, pass the `-s` or `--symbolic` option to the command.

A few other options exist to perform more obscure tasks; consult `ln`'s man page for details.

By default, `ln` creates hard links, which are produced by creating two directory entries that point to the same file (more precisely, the same inode). Both filenames are equally valid and prominent; neither is a "truer" filename than the other, except that one was created first (when creating the file) and the other was created second. To delete the file, you must delete both hard links to the file. Because of the way hard links are created, they must exist on a single low-level filesystem; you can't create a hard link from, say, your root `(/)` filesystem to a separate filesystem you've mounted on it, such as `/home` (if it's a separate filesystem). The underlying filesystem must support hard links. All Linux native filesystems support this feature, but some non-Linux filesystems don't.

Symbolic links, by contrast, are special file types. The symbolic link is a separate file whose contents point to the linked-to file. Linux knows to access the linked-to file whenever you try to access the symbolic link, so in most respects accessing a symbolic link works just like accessing the original file. Because symbolic links are basically files that contain filenames, they can point across low-level filesystems—you can point from the root `(/)` filesystem to a file on a separate `/home` filesystem, for instance. The lookup process for accessing the original file from the link consumes a tiny bit of time, so symbolic link access is slower than hard link access—but not by enough that you'd notice in any but very bizarre conditions or artificial tests. Long directory listings show the linked-to file:

```
$ ls -l alink.odt
lrwxrwxrwx 1 rootsmith users 8 Dec 2 15:31 alink.odt -> test.odt
```

In practice, symbolic links are more common than hard links; their disadvantages are minor, and the ability to link across filesystems and to directories can be important. Linux employs links in certain critical system administration tasks. For instance, System V (SysV) startup scripts use symbolic links in runlevel directories, as described in Chapter 5, “Booting Linux and Editing Files.” Certain commands that have historically been known by multiple names are also often accessible via links. For example, `/sbin/ext2`, `/sbin/fsck.ext3`, and `/sbin/e2fsck` programs are usually links (hard links on some systems, symbolic links on others). You can often leave these links alone, but sometimes you must adjust them. Chapter 5 describes changing the SysV startup script links to affect what programs run when the system boots, for instance.

## Directory Commands

Most of the commands that apply to files also apply to directories. In particular, `ls`, `mv`, `touch`, and `ln` all work with directories, with the caveats mentioned earlier. The `cp` command also works with directories, but only when you use a recursion option, such as `-r`. A couple of additional commands, `mkdir` and `rmdir`, enable you to create and delete directories, respectively.

### The mkdir Command

The `mkdir` command creates a directory. This command's official syntax is as follows:

```
mkdir [options] directory-name(s)
```

In most cases, `mkdir` is used without `options`, but a few are supported:

- **Set mode**: The `-m mode` or `--mode=mode` option causes the new directory to have the specified permission mode, expressed as an octal number. (The upcoming section “Understanding Permissions” describes permission modes.)
- **Create parent directories**: Normally, if you specify the creation of a directory within a directory that doesn't exist, `mkdir` responds with a No such file or directory error and doesn't create the directory. If you include the `-p` or `--parents` option, though, `mkdir` creates the necessary parent directory.

### The rmdir Command

The `rmdir` command is the opposite of `mkdir`; it destroys a directory. Its syntax is similar:

```
rmdir [options] directory-name(s)
```

Like `mkdir`, `rmdir` supports few options, the most important of which handle these tasks:

- **Ignore failures on non-empty directories**: Normally, if a directory contains files or other directories, `rmdir` doesn't delete it and returns an error message. With the `--ignore-fail-on-non-empty` option, `rmdir` still doesn't delete the directory, but it doesn't return an error message.
- **Delete tree**: The `-p` or `--parents` option causes `rmdir` to delete an entire directory tree. For instance, typing `rmdir -p one/two/three` causes `rmdir` to delete `one/two/three`, then `one/two`, and finally `one`, provided no other files or directories are present.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_252_0.png)

When you're deleting an entire directory tree filled with files, `rm -R` is a better choice than `rmdir` because `rm -R` deletes files within the specified directory but `rmdir` doesn't.

## Managing File Ownership

Security is an important topic that cuts across many types of commands and Linux subsystems. In the case of files, security is built on file ownership and file permissions. These two topics are closely intertwined; ownership is meaningless without permissions that use it, and permissions rely on the existence of ownership.

[File ownership] can contain an arbitrary number of users, as described in Chapter 7, “Administering the System.” The two types of ownership enable you to provide three tiers of permissions to control access to files: by the file’s owner, by the file’s group, and to all other users. The commands to manage these two types of ownership are similar, but they aren’t identical.

### Assessing File Ownership

You can learn who owns a file with the `ls` command, which was described earlier. In particular, that command’s `-l` option produces a long listing, which includes both ownership and permission information:

```bash
$ ls -l
total 1141
-rw-r--r--  1 robsmith users 219648 Mar 8 13:06 4425ch02.doc
-rw-r--r--  1 robsmith users 942590 Mar 6 23:31 f0201.tif
```

This long listing includes the username of the owner (robsmith for both files in this example) and the group name of the files’ groups (users for both files in this example). The permission string (`-rw-r--r--` for both files in this example) is also important for file security, as described later in “Controlling Access to Files.”

In most cases, the usernames associated with files are the same as login usernames. Files can, however, be owned by accounts that aren’t ordinary login accounts. For instance, some servers have accounts of their own, and server-specific files may be owned by these accounts.

If you delete an account, as described in Chapter 7, the account’s files don’t vanish, but the account name does. Internally, Linux uses numbers rather than names, so you’ll see numbers in place of the username and group name in the `ls` output. Depending on the file, you may want to archive it, reassign ownership to an existing user, or delete it.

### Changing a File’s Owner

Whenever a file is created, it’s assigned an owner. The superuser can change a file’s ownership using the `chown` command, whose syntax is as follows:

```bash
chown [options] [newowner] [:newgroup] filenames
```

As you might expect, the `newowner` and `newgroup` variables are the new owner and group for the file; you can provide both or omit either, but you can’t omit both. For instance, suppose you want to give ownership of a file to `sally` and the `skyhook` group:

```bash
# chown sally:skyhook forward.odt
```

> **NOTE**  
> Linux’s `chown` command accepts a dot (`.`) in place of a colon (`:`) to delimit the owner and group, at least as of the core file utilities version 6.10. The use of a dot has been deprecated, though, meaning that the developers favor the alternative and may eventually eliminate the use of a dot as a feature.
