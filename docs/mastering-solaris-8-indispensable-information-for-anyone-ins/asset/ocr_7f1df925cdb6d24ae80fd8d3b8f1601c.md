+   2. *Check path names.* Any bad directory entries are removed during the path name check. Should you see a message `ROOT INODE NOT A DIRECTORY (FIX)?`, your file system has sustained substantial damage. After you repair the file system, you should take measures to back up important data and reestablish a fresh file system. Other messages are of minor consequence.

+   3. *Check connectivity.* This part of *fsck* checks to see if there are any directories on your file system that aren't referenced by other directories and are thus orphans. Any directory of this type is placed into the `/lost+found` folder.

+   4. *Check reference counts.* Here *fsck* checks for files that aren't correctly referenced in the file system. These errors are most often corrected automatically, although you may see a message that asks you to clear a file.

+   5. *Check cylinder groups.* In this last phase of the *fsck* operation, the program verifies that the free block and unused inode counts are correct.

+   6. *Salvage free list.* This step corrects the problems found in step 5.

Each step is posted as output of the *fsck* command, with a final line shown that gives you the number of files, the blocks used and free, and how much fragmentation there is. After the sequence of steps for the *fsck* command are complete and when all problems have been corrected, you should see the message `/home: clean` appear.

Fragmentation isn't a major problem on Solaris as it can be on Microsoft Windows. If you have a badly fragmented file system, you can back it up, create a new one, and restore it to defragment it.

You can run *fsck* only on unmounted file systems. On workstations with a single file system or to check all file systems, you should log out of your session and log back into Solaris's command-line prompt in single-user mode as a superuser. Then enter the *fsck* command with any of the options you desire. The syntax for the *fsck* command is as follows:

```
fsck <options> <filesystem list>
```

When you omit `<filesystem list>`, Solaris uses the `/etc/vfstab` file as the source of the file systems to check. Although you can unmount file systems other than the root file system and run the *fsck* command on them, if you want to check and repair the root file system, which cannot be unmounted, you need to be in single-user mode and have the root file system quiescent (in other words, you can't be reading and writing files to root while you are running *fsck*). Many startup scripts specify that *fsck* is run against all file systems before the system is switched into multiuser mode.