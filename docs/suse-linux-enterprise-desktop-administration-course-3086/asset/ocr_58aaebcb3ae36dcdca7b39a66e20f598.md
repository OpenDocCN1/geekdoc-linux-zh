+   6. Verify that the directory was removed by entering
+      ```
+      ls
+      ```
+   7. Remove the `~/my_dir/login` file by entering
+      ```
+      rm ~/my_dir/login
+      ```
+   8. You see a message warning you that the file is write-protected. Confirm the warning by entering `y`.
+   9. Verify that the file has been removed by entering
+      ```
+      ls ~/my_dir/login
+      ```
+   10. Remove all files with names that begin with “a” in the `/home/geeko/my_dir/` directory by entering
+       ```
+       rm -i ~/my_dir/a*
+       ```
+   11. Confirm every warning by entering `y`.
+   12. Remove the `/home/geeko/my_dir/` directory including its content by entering
+       ```
+       rm -r ~/my_dir
+       ```
+   13. Confirm every warning by entering `y`.
+   14. Verify that the directory has been removed by entering
+       ```
+       ls ~/my_dir
+       ```
+   15. Close the terminal window.

# Link Files

File system formats in Linux keep data and administration information separate. How data is organized differs from one file system format to another.

Each file is described by an inode (index node or information node). To see the inode number, you can enter `ls -i`.

Each inode is 128 bytes and contains all the information about this file apart from the filename. This includes information such as details of the owner, access permissions, the size, various time details (time of modification, time of access, time of modification of the inode), and the links to the data blocks of this file.

The ln command creates a link. A link is a reference to a file. Through a link, you can access a file from anywhere in the file system using different names for the file. The file itself exists only once on the system, but it can be found under different names.

Linux recognizes two kinds of links:

+   - Hard links
+   - Symbolic links

You create a *hard link* by using the `ln` command, which points to the inode of an already existing file. Thereafter, the file can be accessed under both names—that of the file and that of the link, and you can no longer discern which name existed first or how the original file and the link differ.