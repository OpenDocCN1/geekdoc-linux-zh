![](bbox=[0.13, 0.09, 0.79, 0.35])

**Figure 25-5.** **SMIT FastPath smitty restfileSYS**

# ## OTHER BACKUP UTILITIES

The **tar**, **pax**, and **cpio** utilities can be used when portability is an issue. Either **pax**, **tar**, or **cpio** will allow you to copy files and directory trees between systems, preserving UIDs and permissions. In some cases, **tar** will not span multiple volumes. Use **cpio** on SySV UNIX machines where **tar** is not available.

```
```
# tar -cvf /dev/rmt0.1 ./source                     Copy to tape
# tar -xvf /dev/rmt0.1                              Restore tar archive
# find . -print | cpio -ov > /dev/rmt0                Copy to tape
# cpio -idmv < /dev/rmt0.1                           Restore cpio archive
```
```

If you have the disk space to spare, you can copy a logical volume using the **cplv** command. This mechanism could be used to create a filesystem copy for backup, leaving the primary copy online.

```
```
# cplv -e <ExistingLV> <SourceLV>                    Copy a logical volume
```
```

As I stated before, **pax** now supports files larger than 2GB. Here are some typical uses for **pax**:

+   - To copy an entire directory structure from one directory to another:
+   ``` 
+   # pax -rw /my_original_dir /my_new_directory
+   ```