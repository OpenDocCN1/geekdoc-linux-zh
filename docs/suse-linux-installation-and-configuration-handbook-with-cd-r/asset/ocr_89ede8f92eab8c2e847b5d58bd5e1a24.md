# Invoking the YaST Backup Module

To start the YaST backup module, you must log in as root and start YaST. Choose System Administration, Create Backups. Alternatively, you can run YaST using the backup mask, which will start YaST in the backup mode immediately. Use the following command to start YaST in backup mode:

```
bash#yast --mask backup
```

# Selecting Directories

At the main backup screen YaST enables you to choose which directories you want YaST to check for creating an optimal backup (see Figure 6.1).

# FIGURE 6.1

You can optimize the backup operation YaST performs by selecting on the right side of the screen the directories YaST should look in. You also can specify that YaST not check mounted devices of the types listed in the left side of the screen.

![](bbox=[0.28, 0.5, 0.78, 0.75])

In some cases, you might have directories that are mount points to other filesystems. For example, say you are mounting a CD-ROM or Windows share. If you do not want YaST to back up the contents of this mount point, you would check the boxes that correspond to the filesystem you do not want YaST to check or include in the backup.

The directory listing on the right side of the screen contains the directories YaST will check for modifications. You can add a directory by pressing the plus (+) key. You will be prompted to enter a path to the directory you want YaST to include in the scan for modifications operation. To remove a directory from the list, highlight it by moving the cursor and pressing the minus (-) key.

> NOTE If you do not optimize the directory listing in which YaST will scan for changes, the search time for changes will be dramatically high. Be sure that the paths YaST will look in are really things you want to back up.

There is no point in backing up the following directories: /tmp, /dev, and /proc. Unless you know what you're doing, do not back them up.