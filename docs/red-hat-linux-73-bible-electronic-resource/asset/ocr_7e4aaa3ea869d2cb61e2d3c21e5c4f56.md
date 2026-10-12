# # Sharing NFS file systems

To share an NFS file system from your Red Hat Linux system, you need to export it. Exporting is done in Red Hat Linux by adding entries into the /etc/exports file. Each entry identifies the directory in your local file system that you want to share. The entry identifies the other computers that can share the directory (or opens it to all computers) and includes other options that reflect permissions associated with the directory.

Remember that when you share a directory, you are sharing all files and subdirectories below that directory as well (by default). So, you need to be sure that you want to share everything in that directory structure. There are still ways to restrict access within that directory structure (those methods are described later).

# ## Configuring the /etc/exports file

As root user, you can use any text editor to configure the /etc/exports file to indicate what directories to share. Here is an example of an /etc/exports file, including some entries that it could include:

```
/cal	*	outdomain.com(rw)	# Company events
/pub	(ro,insecure,all_squash)	# Public dir
/home	maple(rw,squash_uids=0-99)	spruce(rw,squash_uids=0-99)
```

Here is what the entries in the /etc/exports file mean:

+   - **/cal** — Represents a directory that contains information about events related to the company. It is made accessible to everyone with accounts to any computers in the company's domain (*.ourdomain.com). Users can write files to the directory as well as read them (indicated by the rw option). The comment (# Company events) simply serves as a reminder of what the directory contains.

+   - **/pub** — Represents a public directory. It allows any computer and user to read files from the directory (indicated by the ro option), but not to write files. The insecure option lets any computer, even those that don't use a secure NFS port, to have access to the directory. The all_squash option causes all users (UIDs) and groups (GIDs) to be mapped to the anonymous user, giving them minimal permission to files and directories.

+   - **/home** — This is where you enable a set of users to have the same /home directory on different computers. Say, for example, that you are sharing /home from a computer named oak. The computers named maple and spruce could each mount that directory on their own /home directory. If you gave all users the same user name/UIDs on all machines, you could have the same /home/user directory available for each user, regardless of which computer they logged in to. The uids=0-99 is used to exclude any administrative login from another computer from changing any files in the shared directory.