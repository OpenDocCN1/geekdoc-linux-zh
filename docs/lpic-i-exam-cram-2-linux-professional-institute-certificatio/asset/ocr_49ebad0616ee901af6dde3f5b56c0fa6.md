+   4. You require your system to check a particular file system every 50 times the file system is mounted. Which command would you use to make this change?
+   
+   - A. `debugfs`
+   - B. `dumpe2fs`
+   - C. `tune2fs`
+   - D. `setfs`

Answer C is correct because the maximum mount count option can be set with the `tune2fs` command. Answer A is incorrect because the `debugfs` command manipulates the file system modes and contents but not the needed parameter. Answer B is incorrect because the `dumpe2fs` command shows only parameters for the file system. Answer D is incorrect because the `setfs` command doesn't exist.

+   5. A user reports that one of his fellow users is hogging all the disk space on their shared server. Which command would you use to show that system's disk statistics for its mounted file systems?
+   
+   - A. `dir`
+   - B. `df`
+   - C. `du`
+   - D. `ls`

Answer B is correct because the `df` command shows the disk statistics for mounted file systems. Answer A is incorrect because `dir` is only an alias for the `ls` command. Answer C is incorrect because the `du` command can show the space used by files, but not disk statistics like `df` can. Answer D is incorrect because the `ls` command can show file sizes but not disk statistics.

6. What is the device name of the third SCSI device on a Linux system? Fill in the blank with the full path and filename of the device:

![](bbox=[0.14, 0.72, 0.9, 0.74])

The correct answer is /dev/sdc. There are no alternative answers.

+   7. Which portion of a file's information is not stored in the `inode` or `data blocks`?
+   
+   - A. Link count
+   - B. Link permissions
+   - C. Filename
+   - D. Owner

Answer C is correct because the filename is not stored with the `inode` or in the data location for the file; it occurs only in the directory file that contains the filename entry. Answer A is incorrect because the link count affects only hard links and is shown by the `stat` command. Answer B is incorrect because link permissions affect only a symbolic