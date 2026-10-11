again, you see another message, such as NFS server speedy OK. Setting up a stable network and server (or not using NFS) is the best defense against these kinds of problems.

**Security** NFS is based on the trusted-host paradigm (page 376) and therefore has all the security shortcomings that plague other services based on this paradigm. In addition, NFS is not encrypted. Because of these issues, you should implement NFS on a single LAN segment only, where you can be (reasonably) sure that systems on a LAN segment are what they claim to be. Make sure a firewall blocks NFS traffic from outside the LAN and never use NFS over the Internet.

To improve security, make sure UIDs and GIDs are the same on the server and clients (page 741).

# ## MORE INFORMATION

**Web** nfs.sourceforge.net

**HOWTO** NFS HOWTO  
Netboot and PXE: Remote-Boot mini-HOWTO

**Book** NFS Illustrated by Callaghan, Addison-Wesley (December 1999)

# # SETTING UP AN NFS CLIENT

This section covers setting up an NFS client, mounting remote directory hierarchies, and improving NFS performance.

# ## PREREQUISITES

Install the following packages:

+   - **nfs-utils**
+   - **system-config-nfs** (optional)

Under *RHEL*, the **portmap** utility (part of the **portmap** package; refer to “RPC Network Services” on page 391) must be running to enable reliable file locking. Under *FEDORA*, this function is served by **rpcbind**.

There are no daemons to start for NFS clients.

# ## JUMPSTART I: MOUNTING A REMOTE DIRECTORY HIERARCHY

To set up an NFS client, mount the remote directory hierarchy the same way you mount a local directory hierarchy (page 487). The following sections detail this process.

# ### mount: MOUNTS A REMOTE DIRECTORY HIERARCHY

The following examples show two ways to mount a remote directory hierarchy, assuming that **speedy** is on the same network as the local system and is sharing /home and /export with the local system. The /export directory on **speedy** holds two directory hierarchies that you want to mount: /export/progs and /export/oracle.