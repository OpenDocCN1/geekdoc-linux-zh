# Configuring the /etc/exports file

The shared directory information you entered into the NFS Server Configuration window is added to the /etc/exports file. Root user, you can use any text editor to configure the /etc/exports file to modify shared directory entries or add new ones. Here's an example of an /etc/exports file, which could include:

```
/cal *.linuxutoys.net (rw,sync)      # Company events
/pub (ro,insecure,all_squash)      # Public dir
/home maple(rw,squash uids=0-99) spruce(rw,squash uids=0-99)
```

The following text describes these entries:

+   - cal Represents a directory that contains information about events related to the company. It is made accessible to everyone with all computers in the company's domain (*linuxutoys.net). Users can write files to the directory as well as read them (the rw option).

+   The sync option, which is the default behavior, is explicitly here to indicate that NFS will only reply to new requests after changes have been committed to storage. The alternative is to use async, which allows new requests before changes are committed to improve performance, but can result in data corruption.) The comment (# Company events) simply reminds you of what the directory contains.

+   - pub Represents a public directory. Any computer and user can read files from the directory (by the ro option), but not to write files. The insecure option enables any computer, even one that doesn't use a NFS port, to access the directory. The all_squash option allows all users (UIDs) and groups (GIDs) to be mapped to the nfsnobody user, giving them minimal permission to files and directories.

+   - home This entry allows a set of users to share the same /home directory on different computers. Say, for example, that you are sharing /home from a computer named Oak. The computers maple and spruce could each map that directory on their own /home directory. If you give all the same user name/UIDs on all machines, you could have the same /home/user directory available for each user, regardless of which computer they logged into. The uids=0-99 is used to exclude any administrative login from another computer from changing files in the shared directory.

Of course, you can share any directories that you choose (these were just examples), including the entire file system(/). There are security implications of sharing the whole file system or sensitive parts of it (such as /etc). Security options that you can add to your /etc/exports file are described throughout the sections that follow.

The format of the /etc/exports file is:

```
Directory Host (Options) # Comments
```