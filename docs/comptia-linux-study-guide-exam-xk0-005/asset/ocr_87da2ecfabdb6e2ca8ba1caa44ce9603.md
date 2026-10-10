# # Replicating with rsync

Originally covered in Chapter 3, “Managing Files, Directories, and Text,” the `rsync` utility is known for speed. With this program, you can copy files locally or remotely, and it is wonderful for creating backups.

Before exploring the `rsync` program, it is a good idea to review a few of the commonly used options. Table 3.4 in Chapter 3 contains the more commonly used `rsync` options. Besides the options listed in Table 3.4, there are a few additional switches that help with secure data transfers via the `rsync` utility:

+   - The `-e`, or `-rs`, option changes the program to use for communication between a local and remote connection. The default is OpenSSH.
+   - The `-z`, or `--compress`, option compresses the file data during the transfer.

Back in Chapter 3 we briefly mentioned the archive option, `-a` (or `--archive`), which directs `rsync` to perform a backup copy. However, it needs a little more explanation. This option is the equivalent of using the `-rlptgoD` options and does the following:

+   - Directs `rsync` to copy files from the directory’s contents and for any subdirectory within the original directory tree, consecutively copying their contents as well (recursively).
+   - Preserves the following items:

+     - Device files (only if run with super user privileges)
+     - File group
+     - File modification time
+     - File ownership (only if run with super user privileges)
+     - File permissions
+     - Special files
+     - Symbolic links

It’s fairly simple to conduct `rsync` backup locally. The most popular options, `-ahv`, allow you to back up files to a local location quickly, as shown in Listing 12.15.

**Listing 12.15** Using `rsync` to back up files locally

```
```bash
$ ls -sh *.tar
40K Project4x.tar   40K ProjectVerify.tar
$
$ mkdir TarStorage
$
$ rsync -ahv *.tar TarStorage/
sending incremental file list
Project4x.tar
ProjectVerify.tar
```
```