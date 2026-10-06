# Working with NFS and NIS

NFS is the Network File System, which was pioneered by Sun and has become a standard in the world of Unix. With NFS, clients can mount filesystems across the network that are being offered by NFS servers and work with them as if they were filesystems mounted from local disks. NIS is a simple and widely used method of sharing files across the network.

NIS is a distributed authentication mechanism that developed as a companion to NFS. NIS provides an easy, centralized way of using the same user and group accounts and system configuration information within a network of systems running NFS. This eliminates the need for a system administrator to manually synchronize and update user and group accounts across all of the systems on a network.

In this chapter, we look at how to mount NFS filesystems on clients systems and how to set up an NFS server to make worked filesystems available (known as exporting them). We then explore how to set up an NIS server and share the authentication and system information that it provides for all of the NFS clients on your network.

# Mounting NFS Filesystems

A machine that is offering directories to share across the network by NFS is an NFS server. A machine that mounts one of these shares for its own use is an NFS client.

# CHAPTER 22

# In This Chapter

+   - Mounting NFS filesystems across the network

+   - NFS mount options

+   - Setting up an NFS server

+   - Solving problems with NFS

+   - NIS security

+   - Using NIS for authentication

+   - Setting up an NIS server

+   - Configuring NIS clients