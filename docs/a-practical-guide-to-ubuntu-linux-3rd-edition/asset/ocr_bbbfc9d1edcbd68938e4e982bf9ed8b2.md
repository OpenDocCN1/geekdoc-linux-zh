hard disks and printers. Inodes, which are identified by inode numbers, are stored on disk and define a file's existence. When the system comes up, the `/etc/fstab` file controls which filesystems are mounted and how they are mounted (readonly, read-write, and so on). After a system crash, filesystems are automatically verified and repaired if necessary by `fsck`. You can use `tune2fs` to force the system to cause `fsck` to verify a filesystem periodically when the system boots.

# EXERCISES

+   1. What is the function of the `/etc/hosts` file? Which services can you use in place of, or to supplement, the **hosts** file?
+   2. What does the `/etc/resolve.conf` file do? What do the **nameserver** lines in this file do?
+   3. What is an inode? What happens to the inode when you move a file within a filesystem?
+   4. What does the `..` entry in a directory point to? What does this entry point to in the root (`/`) directory?
+   5. What is a device file? Where are device files located?
+   6. What is a FIFO? What does FIFO stand for? What is another name for a FIFO? How does a FIFO work?

# ADVANCED EXERCISES

+   7. Write a line for the `/etc/fstab` file that mounts the `/dev/hdb1` **ext4** filesystem on `/extra` with the following characteristics: The filesystem will not be mounted automatically when the system boots, and anyone can mount and unmount the filesystem.
+   8. Without using `rm`, how can you delete a file? (*Hint:* How do you rename a file?)
+   9. After burning an ISO image file named `image.iso` to a CD on `/dev/hdc`, how can you verify the copy from the command line?
+   10. Why should `/var` reside on a separate partition from `/usr`?
+   11. Create a FIFO. Using the shell, demonstrate that two users can use this FIFO to communicate asynchronously.
+   12. How would you mount an ISO image so you could copy files from it without burning it to a CD?