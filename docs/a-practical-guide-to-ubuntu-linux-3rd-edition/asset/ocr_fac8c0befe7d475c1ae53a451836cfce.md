# ### ENABLING ACLs

Before you can use ACLs you must install the acl software package:

```
$ sudo aptitude install acl
```

Ubuntu Linux officially supports ACLs on **ext2**, **ext3**, and **ext4** filesystems only, although informal support for ACLs is available on other filesystems. To use ACLs on an **ext2/ext3/ext4** filesystem, you must mount the device with the **ad** option (**no\_acl** is the default). For example, if you want to mount the device represented by /home so that you can use ACLs on files in /home, you can add **ad** to its options list in /etc/fstab:

```
$ grep home /etc/fstab
LABEL=/home			/home			 ext4	 defaults,ac1	 1 2
```

**remount** option	After changing fstab, you need to remount /home before you can use ACLs. If no one else is using the system, you can unmount it and mount it again (working with root privileges) as long as the working directory is not in the /home hierarchy. Alternatively you can use the **remount** option to mount to remount /home while the device is in use:

```
$ sudo mount -v -o remount /home
/dev/sda3 on /home type ext4 (rw,ac1)
```

See page 510 for information on fstab and page 506 for information on mount.

# ## Working with Access Rules

The setfacl utility modifies a file's ACL and getfacl displays a file's ACL. When you use getfacl to obtain information about a file that does not have an ACL, it displays the same information as an ls-l command, albeit in a different format:

```
$ ls -l report
-rw-r--r-- 1 max max 9537 2010-01-12 23:17 report

$ getfacl report
# file: report
# owner: max
# group: max
user::rw-
group::r--
other::r--
```

The first three lines of the getfacl output comprise the header; they specify the name of the file, the owner of the file, and the group the file is associated with. For more information refer to “ls -l: Displays Permissions” on page 215. The **--omit-header** (or just **-o**) option causes getfacl not to display the header:

```
$ getfacl --omit-header report
user::rw-
group::r--
other::r--
```