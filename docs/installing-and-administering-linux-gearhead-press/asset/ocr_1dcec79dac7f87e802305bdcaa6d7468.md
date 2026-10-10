+   move ahead (with less, ahead and back) at your own pace.
+   Therefore, it is a lot easier to read.

+   25. You cannot remove the directory because it is not empty. After you remove the files from goodstuff, you can remove the directory. Note that if a directory contains only the .. and . special files, it is considered empty, so removal is not impeded.

+   28. The name of the command is date, and the command is found in /usr/bin.

+   29. At the top of the date command’s first page, you read that the information has been taken from the sh-utils.info file and that the node name is date invocation. The name of the next node is uname invocation.

# ## Chapter 6

+   3. Creating zero-length files.

+   4. There is no difference in the file information. Both correspond to the same physical file; it is just that the file has two different filenames. You can check this information by executing ls -1i to get the inode number for each filename. You will see that each file has the same inode number.
+   An ordinary file has a link count of 1. A file with a single link to it has a link count of 2. Both the original mycal file and its link have link counts of 2.

+   5. The output is identical to the output of mycal, which is a display of the calendar of the current month. You cannot execute the mycal command. You will get a reply from Linux of bash: myscripts/mycal: Permission denied. Changing the permissions to read-only on the linked filename is the same as changing permissions on the file to the (original) file itself.

+   6. No, removing the linked filename does not remove the original file to which it is linked. Removing home_mycal simply removes the directory entry in the myscripts directory that refers to homemycal and changes the link count from 2 to 1. The ./myscripts/mycal file remains intact. If you execute an ls -1 on the original file, however, you will see that the link count is reduced.