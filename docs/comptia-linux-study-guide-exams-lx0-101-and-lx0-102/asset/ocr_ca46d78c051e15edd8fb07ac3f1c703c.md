# Using File Management Commands

```
$ ls -l alink.odt
lrwxrwxrxr-x 1 rodsmith 8 Dec 2 15:31 alink.odt -> test.odt
```

In practice, symbolic links are more common than hard links; their disadvantages are minor, and the ability to link filesystems and to directories is Important. Linux employs links in certain critical system administration tasks. For instance, System V (SysV) startup scripts use symbolic links in runlevel defaults, as described in Chapter 5, “Booting Linux and Editing Files.” Certain commands have historically been known by multiple names and are also accessible via links. For example, the /sbin/fsck.ext2, /sbin/fsck.ext3, /sbin/e2fsck programs are usually (hard links on some systems, symbolic links on others). You can often leave these alone, but sometimes you may just adjust them. Chapter 5 describes changing the SysV startup script links to affect what programs run when the system boots, for instance.

# Directory Commands

Most of the commands that apply to files also apply to directories. In particular, 1s, mv, touch, and in all work with directories, with the caveats mentioned earlier. The cp command also works with directories, but only when you use a recursion option, such as -r. A couple of additional commands, mkdir and rmdir, enable you to create and delete directories, respectively.

# The mkdir Command

The mkdir creates a directory. This command's official syntax is as follows:

```
mkdir [options] directory-name(s)
```

In most cases, mkdir is used without options, but a few are supported:

**Set Mode** The -m mode or --mode option creates the new directory to have the specified permission, expressed as an octal number.(The upcoming section “Understanding Permissions” describes permission modes.)

**Create Directories** Normally, if you specify the creation of a directory within a directory that doesn't exist, mkdir responds with a No such file or directory error and doesn't create the directory. If you include the -p or --parents option, then, mkdir creates the necessary parent directory.

# The rmdir Command

The rmdir command is the opposite of mkdir; it destroys a directory. Its syntax is similar:

```
rmdir [options] directory-name(s)
```