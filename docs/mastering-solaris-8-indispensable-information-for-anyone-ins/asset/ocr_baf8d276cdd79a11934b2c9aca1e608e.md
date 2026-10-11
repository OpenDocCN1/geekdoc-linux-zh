**WARNING** If you run `fsck` on a mounted file system, you can damage that file system so that it is unusable. Press Ctrl+C to terminate the `fsck` command as quickly as you can to prevent any damage.

There are numerous options and suboptions for the `fsck` command. Among the most important are those listed here:

+   - `-F <file system type>` option   Check for only this type of file system.
+   - `-m` option       Check that the file system can be mounted.
+   - `-n` option       Answer no to any question posed by `fsck`.
+   - `-of` option     Force `fsck` to skip clean or checked file systems.
+   - `-op` (**or preen**) **option**  Run `fsck` so that it automatically repairs any errors it finds. If there is an error that can't be fixed and requires user intervention, this option forces `fsck` to quit or exit.

# ## Summary

This chapter described the various file systems in use by Solaris 8 and how they're used. Solaris uses many different file system types, both real and virtual. Some file systems mount automatically, and others require manual mounting and unmounting. The file system hierarchy is a tree structure with the root directory at the top of the tree. File-names, file types, path names, and file attributes provide ways to describe files that allow them to be stored in the file system, retrieved, and recognized for the data they contain.

Directories are containers that store files and other directories. This chapter listed the important directories and files that Solaris contains. I discussed working with directories, files, and links and showed you how to create, copy, move, and delete them both in Command Line Interface (CLI) operations and through the CDE.

I also discussed access rights and permissions, which provide a scheme for protecting files and directories by setting security as well as determining what operations may be performed on an object.

Finally, this chapter include a discussion of disk storage structures, inodes, and blocks, which provide a means to store data on disk and relate the data to a file system so that the data may be used when needed. You learned about several commands you can use to determine your disk and file utilizations as well as set disk quotas to limit disk usage by specific users.