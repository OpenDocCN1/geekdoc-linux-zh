> **ALERT**
> The name of a file is the only thing about the file not stored in the inode. This appears on the exam in questions for this set of objectives.

Hard links can't be created if the target is on another file system, disk, or remote object. The need to hook multiple names to the same inode makes this impossible.

Be careful when changing the permissions and ownership on the hard-linked files because all name entries point to exactly the same inode. Thus, any changes are instantly made to what would appear to be multiple files but what, in reality, are only filenames.

To delete a file that has multiple hard links requires the removal of every hard link or the multiple names. To find all the links for a file, run the following command:

```
```
is -i ccontactlist.txt
17392 ccontactlist.txt
find / -inum 17392
/home/jaime/cccontactlist.txt
/backup/home/jaime_cccontactlist.txt
```
```

> **ALERT**
> On the exam, remember that a symlink is another actual file with its own inode. A large amount of symlinks can therefore cause a problem for a file system, such as one that contains users' home directories. Too many inodes used can restrict you from using the storage space that's available. Run the df -i command to see what the statistics are.

# # Working with Permissions

Permissions determine how users can access resources on the system. System security is configured by the user's UID (User ID), her GIDs (Group ID), (both primary and secondary), and the permissions on the object she is attempting to access.

# ## Permission Trio Bits

Figure 6.3 shows the 10 positions (1 type bit and 3 trios of permission bits) that make up the permissions section of a file.

![](bbox=[0.08, 0.85, 0.55, 0.94])

**Figure 6.3** Permission trios.