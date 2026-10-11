Table 16-21 (continued)  

| Option | Function |
| :--- | :--- |
| -z | Zero the kernel statistics counters. |
| -o <facility> | Show only the requested facility. Available facilities are as follows: | 
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; nfs | NFS protocol information | 
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; rpc | RPC information | 
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; net | Network layer statistics and information | 
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; fh | File handler information | 
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; rc | Request reply cache information |

# Security considerations

NFS was not designed with security in mind, and special attention must be paid to secure an NFS system. NFS uses the UID (user ID) and GIDs (group IDs) of the user on the client to grant permissions. The UID is the numeric number that represents a user in the /etc/passwd file, and the GID is the numeric number that represents a group in /etc/group. The client UID and GUID are matched to the local IDs in /etc/passwd and /etc/group. The only way to have a secure NFS setup is to make sure all IDs match on all systems. A user should always have the same number. Also consider that users have root access on their workstations, they can change to any ID they want and impersonate any users they want to.

Access by remote systems can be controlled by restrictions in the /etc/exports file. As another precaution, you should always block or filter the NFS and RPC ports for any servers exporting directories. Even though you can limit which clients connect, it is not out of the question for a DNS server to be compromised and hostnames or domain names changed to allow unwanted access. Table 16-22 shows the ports that should be blocked.

Table 16-22
NFS Ports  

| Port | Protocol(s) | Process |
| :--- | :--- | :--- |
| 111 | TCP and UDP | portmapper |
| 745 | UDP | mountd |
| 747 | TCP | mountd |
| 2049 | TCP and UDP | nfsd |