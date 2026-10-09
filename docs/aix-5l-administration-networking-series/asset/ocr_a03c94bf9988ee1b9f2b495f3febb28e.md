HANFS also supports the automatic reintegration of the primary server once the problem failure has been rectified and the system is back online. Basically, the procedure described in the previous paragraph is reversed, and the servers go back to doing their old jobs. Note that no changes to standard NFS client software is required to make use of HANFS services. HANFS will work fine with your Sun, HP, DEC, and other standard (grain of salt here) NFS clients and servers.

# CHECKLIST

The following is a checklist for the key points in Networked Filesystems: NFS, NIS, and NIS+:

+   - Define a virtual filesystem (VFS).

+   - Identify the client/server architecture that is the basis for NFS.

+   - Define the NFS server and identify its design.

+   - Improve performance by using the NFS clients to implement client-side data caching.

+   - Simplify system administration by using Network Information Services NIS to centralize the information about systems and users in a network.

+   - Begin troubleshooting problems by listing and verifying the current set of client mounts known to the server.

+   - Use the High-Availability Network Filesystem (HANFS) to provide an extension to standard NFS services that allows a second RS/6000 or pSeries to act as a backup NFS server should the primary NFS server fail.

+   - Share NFS server CPU cycles and memory between all operating system components.