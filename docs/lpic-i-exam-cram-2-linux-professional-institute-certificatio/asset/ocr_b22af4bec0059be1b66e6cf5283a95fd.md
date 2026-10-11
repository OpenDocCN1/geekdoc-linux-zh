# Hard Links

*A hard link* is normally used to create a backup or an anchor of an important file to which users must have read-write access. A hard link is simply an additional name in a directory file that points to the exact same inode and shares every aspect of the original file except the actual name. Figure 6.2 shows the relationship between a hard link and the target file.

![](bbox=[0.07, 0.24, 0.55, 0.46])

**Figure 6.2** Hard link detail.

For an example of using a hard link, consider the need to ensure that a frequently deleted file is easily restorable for a given user. The user, Jaime, travels a lot, but when he's in the office he seems to delete things a lot or claims the system has eaten his files. When Jaime is flying, you don't have any issues, so the problem must be the user's actions.

To anchor or back up an important file such as the company contact list in Jaime's home directory, you first must create a backup directory, something like /backup.

Then, you create a hard link from Jaime's ccontactlist.txt file to a file in the /backup directory, like so:

```
```
cd -jaimenin
ln ccontactlist.txt /backup/home_jaime_ccontactlist.txt
ls -li ccontactlist.txt
-rw-rw.2 jaim users 0 Jan 26 13:08 ccontactlist.txt
```
```

Notice that the file appears normal, but the number 2 for the link count lets you know that another name entry for this file exists somewhere.

Also notice that the listing for the new hard link doesn't show the target file, or seem to refer to it in any way. Running the stat command on this file won't show you the other filename or seem to be aware of it outside of the higher link count.