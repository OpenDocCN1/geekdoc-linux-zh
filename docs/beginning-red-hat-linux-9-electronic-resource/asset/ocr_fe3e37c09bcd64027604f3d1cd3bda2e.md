```
$ ln -s /boot/boot.b boot.b_soft
$ ls -al boot.b_soft
lrwxrwxrwx 1 deeptak users 12 Jan 19 20:21 boot.b_soft -> /boot/boot.b
```

When we attempt to create a hard link to a file on a different partition, the operating system does not allow us to do so. This is because inode numbers are unique only within a partition and a hard link requires the same inode number as the link target, which may not be possible on a different partition. However, we are able to successfully create a symbolic link to a file on a different partition.

Links are commonly used for organizing shared directories. For instance, a project group may choose to share files in a directory called `/var/documents`. Users who wish to share documents may choose to leave the documents in any subdirectory under their own home for ease of maintenance. This is how a typical directory structure would look like in this case:

```
$ ls -l /var/documents
total 0
lrwxrwxrwx 1 deeptak users 22 Feb 23 23:54 deeptak ->
/home/deeptak/joe_docs

lrwxrwxrwx 1 zora users 18 Feb 23 23:55 zora ->
/home/zora/work/blueprints

lrwxrwxrwx 1 sarah users 18 Feb 23 23:55 sarah ->
/home/sarah/deep down/mydocs
```

Members of the group may choose to maintain their documents in any sub-directory under their home directory. They still have the convenience of referring to a colleague's shared documents by accessing `/var/documents/<user name>`. A new project member, say with the user name apprentice, would typically execute the following command to add her document directory to this scheme of things:

```
$ ln -s mydocdir /var/documents/apprentice
```

For this scheme to work, the owner of the `/var/documents` directory should allow members of the project group write permissions for the `/var/documents` directory. We shall see more about groups and permissions in the next section.

# ## Ownership of Files

Every file stored on a Linux system has an owner – this indicates the creator of the file. Each file also has the notion of a group associated with it. A group is essentially a group of users (a number of groups exist on the system by default – including the groups users, administrators, and daemon). The file /etc/group has a complete list of available groups on the system: