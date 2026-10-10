note that NFS has several disadvantages. Improperly configured, NFS can open security holes that a knowledgeable intruder could exploit. In addition, NFS does not provide a straightforward method to integrate Microsoft Windows 95/98/NT systems; if you would like to include Windows machines in your network, see the section “Configuring Samba Networking,” later in this chapter.

# # Configuring NFS: An Overview

To get NFS working successfully, you must do the following:

+   1. Make sure that your user and group IDs match on the client and server systems.
+   2. On the server, modify /etc/hosts.allow and /etc/hosts.deny so that the server will accept portmap requests from clients on your network.
+   3. On the server, create or modify the file /etc/exports so that the server will make specified directories available to other machines on the network.
+   4. On the client, modify /etc/fstab so that the client will automatically load the exported directories when you start the client system.

# ## User and Group IDs

NFS won’t work smoothly (or at all) if the user and group names and numerical IDs aren’t the same on both systems. If there are discrepancies, you must fix them before proceeding. See usermod (Chapter 12) for information on changing the UID and GID of users. Also see chmod (Chapter 5) for information on changing the ownership of files recursively throughout the user’s directories.

> **TIP** If you change a user’s IDs, all of the user’s files must be modified (with **chmod**, discussed in Chapter 5) to match the new user and group IDs.