In the last step of the backup procedure, you should specify the archive name. If you choose, you also can specify the options for the archive and the file listing file path (see Figure 6.4). The following are the options for the archive:

# FIGURE 6.4

You can specify archive-specific information by filling in the information required in this screen. The information you supply to YaST in this dialog will be passed to the tar command to generate the archive.

![](bbox=[0.26, 0.27, 0.75, 0.58])

+   - **Archive name**—This is the name of the archive that will be created in the absolute path. Archive names usually end with a .tar extension, or .tar.gz if you choose the Compress Archive option. You can specify the archive to be saved on a tape by passing /dev/tape/archivename.tar, which tells YaST to make the archive on tape.
+   - **Compress archive**—This option tells YaST to compress the archive. You can decrease the space needed for the archive by using this option.
+   - **List of contents**—When checked, YaST will be verbose when adding the files to the archive.
+   - **List of contents**—When checked, you should enter a filename in the in file field. YaST will save a list of the filenames archived to this file.

After you have filled in the values, YaST will start backing up the files to the archive name you selected.

# Restoring Files

To restore files from a tarball backup file, you should use the tar command. In the following example, we assume that the archive is located on /dev/tape. The following command restores all the files from the tape to their original location:

```
bash#tar xvf /dev/tape -C /
```

If the stored archive is a compressed archive, you should use the following command instead:

```
bash#tar xzvf /dev/tape -C /
```

If a system failure occurs in which you have to reinstall the whole system, the previous method works best. If you want to be selective when choosing files to restore out of an archive, you can learn more about tar in Appendix E. “Various Utilities.”