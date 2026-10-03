3. Check the new file system using fsck as follows:

```
fsck /dev/rdsk/c?t?d?s?
```

4. Mount the file system to be restored, and change to that directory:

```
mount /dev/dsk/c?t?d?s? <directory>
cd /<directory>
```

5. Load the tape, and issue the following command:

```
ufsrestore rf /dev/rmt/0
```

The entire contents of the tape will be restored to the file system. All permissions, ownerships, and dates will remain as they were when the last incremental tape was created.

The next two steps are optional.

6. Remove the restoresymtable file created by the ufsrestore command. This is a temporary file, and is not required after the file system has been successfully restored.

7. It’s also a good idea to unmount the file system and run fsck again to check the repaired file system.

# Recovering the Root or /usr File System

Sometimes a careless administrator with root access accidentally deletes part or all of the root (/) or /usr file system. Other times, the file system can become unusable because of a faulty disk drive or a corrupted file system. Follow this procedure if you ever need to recover the root (/) or /usr file system:

# STEP BY STEP

# 11.2 Recovering the Root or /usr File System

1. Replace and partition the disk if it has failed.

2. Re-create the file system by issuing the newfs command as follows:

```
newfs /dev/rdsk/<disk-partition-name>
```