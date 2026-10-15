once a file has been deleted, the only way to recover it is from archival backups that you or the system administrator have made of the file system.

```
$ cd
$ rm myfile2
rm: myfile2: No such file or directory
$
```

You get the error message because in the home directory, the file named myfile2 does not exist. It was moved down into the subdirectory named first.

Directory organization also includes the ability to delete empty or nonempty directories. The command that accomplishes the removal of empty directories is rmdir. The general syntax of the rmdir command is as follows:

# SYNTAX

```
rmdir [options] dirnames
```

+   **Purpose:** Removes the empty directories specified in dirnames
+   **Output:** Removes directories
+   **Commonly used options/features:**
+   - **-p** Remove empty parent directories as well
+   - **-r** Recursively delete files and subdirectories beneath the current directory

To delete an entire directory below the current working directory, type the following:

```
$ rmdir first
rmdir: first: Directory not empty
$
```

Since the file myfile2 is still in the subdirectory named first, first is not an empty directory, and you get the error message that the rmdir command will not delete the directory. If the directory was empty, rmdir would have accomplished the deletion. One way to delete a nonempty directory is by using the rm command with the -r option. The -r option recursively descends down into the subdirectory and deletes any files in it before actually deleting the directory itself. Be cautious with this command, since you may inadvertently delete directories and files with it. To see how this command deletes a nonempty directory, type the following:

```
$ rm -r first
$
```

The directory first and the file myfile2 are now removed from the file structure.

# 2.4.5 Obtaining Help with the Man Command

A very convenient utility available on UNIX systems is the online help feature, achieved via the use of the man command. The general syntax of the man command is as follows: