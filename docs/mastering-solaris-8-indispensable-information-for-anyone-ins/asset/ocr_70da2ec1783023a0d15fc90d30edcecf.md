To restore an entire file system from backup, follow these steps:

+   1. Log in as superuser.

+   2. Use the change directory command cd `<pathname>` to switch to the directory on which the file system is mounted.

+   3. Issue the following command:
+   
+   ```
+   # ufsrestore if /dev/rmt/0
+   ```

Here the i option starts the ufsrestore command in the interactive mode, which allows you specify which files and directories should be restored. The f option specifies the device (/dev/rmt/0) that the backup tape is mounted on.

The ufsrestore command restores the dump with the number that is higher than the number of the dump that was restored the last time ufsrestore was used. If there is more than one ufsrestore used at the same level in the restore hierarchy, the command restores the most recent dump at that level.

The ufsrestore r option will restore your file system automatically without intervention, as follows:

```
# ufsrestore rf /dev/rmt/0
```

After a ufsdump or ufsrestore command is completed, tape drives typically rewind to the beginning of the tape. You can specify that the tape not rewind by appending the n option to the device command, as in /dev/rmt/0n. The n option is particularly useful when you're using the ufsdump or ufsrestore command to write to or read from remote tape drives in a sequential fashion, something you might do when you want to back up or restore multiple file systems to a volume.

![](bbox=[0.17, 0.67, 0.21, 0.71])

**TIP** Use the man mtio command to view the magnetic tape I/O interface and option man page. This page documents options that help you work with tape drives.

If you wish to restore a single file on tape using ufsrestore, use the x option and input the filenames from the command line. You must be in the same working directory that you wish the restored file to appear in when you use the command, as shown here (where the /<pathname>/<directoryname>/<Filename> argument is the file that is to be restored from tape):

```
# cd /<directoryname>
# ufsrestore xf /dev/rmt/0 <pathname>/<directoryname>/<filename>
```