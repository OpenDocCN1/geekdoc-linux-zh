+   5. Display the total disk usage of all files and directories, and show the grand total at the end:

```
du -h -c /path/to/directory1 /path/to/directory2
```

# **19. tar: Create or extract tar archives.**

The `tar` command in Linux is used for creating and manipulating archive files. It stands for "tape archive" and is commonly used to bundle multiple files and directories into a single archive file. The `tar` command is particularly useful for compressing and backing up data.

**Examples:**

+   1. **Create a Tar Archive:**

```
tar -cvf archive.tar file1.txt file2.txt directory/
```

This command creates a tar archive named `archive.tar` containing `file1.txt`, `file2.txt`, and the contents of the `directory/`.

+   2. **Extract Files from Tar Archive:**

```
tar -xvf archive.tar
```