# Chapter 27 ✦ Running a File Servers

Remember when you share a directory, you are sharing all files and subdirectories below that directory as well (by default). So, you need to be sure that you want to share everything in that directory structure. There are still ways to restrict access within that directory structure, and those are discussed later in this chapter.

# Configuring the /etc/exports File

To make a directory from your Linux system available to other systems, you need to export it. Exporting is on a permanent basis by adding information about an exported directory to the /etc/exports file.

The format of the /etc/exports file is

```
Directory Host(Options) # Comments
```

where Directory is the name of the directory that you want to share, and Host indicates the computer to which the sharing of this directory is restricted. Options can include a variety of options to define the security measures attached to the shared directory for the host. (You can repeat Host/Option pairs.) Comments are any optional comments you want to add (following the #).

As root user, you can use any editor to configure /etc/exports to modify shared entries or add new entries. Here's an example of an /etc/exports file:

```
/cal *.linuxtoys.net(rw) # Company events
/pub (ro.Insecure,all_squash) # Public dir
/home maple(rw,squash uids=0-99) spruce(rw,squash uids=0-99)
```

The cal entry represents a directory that contains information about events related to the company. It is made accessible to everyone with any computers in the company's domain (*.linuxtoys.net). Users can write to the directory as well as read them (indicated by the rw option). The (# Company events) simply serves to remind you of the directory contents.

The /pub entry allows any company and user to read files from the directory (indicated by the ro option) but not to write files. The insecure port enables any computer, even one that does not use a secure NFS port, to access the directory. The all_squash option uses all users (UIDs) and groups (GIDs) to be mapped to the nfsnobody user, giving minimal permissions to files.

The /home entry enables sets of users to have the same /home directory on different computers. For example, that you are sharing /home from a computer named oak. The computers named maple and spruce could each mount that on their own home directories. If you give all users the same username/UIDs on all machines, you could have the same /home/user directory available for each user, regardless of which computer they are logged into. The ids=0-99 is used to exclude any administrative login from another computer from changing files in the shared directory.