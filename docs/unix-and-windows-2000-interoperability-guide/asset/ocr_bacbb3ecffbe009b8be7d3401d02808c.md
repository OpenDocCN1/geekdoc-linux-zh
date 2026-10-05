Windows 2000 NFS Server/HP-UX NFS Client

# 11.4.1.2 Logging, Locking, and Client Groups

The SFU Administration MMC also enables you to configure logging, locking, and client groups. You can easily configure the logging of the following events:

+   - Mount. Users making mount and unmount requests.
- Locking. Users locking and unlocking files.
- Read. Users making requests to read a file.
- Write. Users making requests to write to a file.
- Create. Users making requests to create a file.
- Delete. Users making requests to delete a file.
- All. All of the above.

Just click on the Logging tab of the SFU MMC to configure logging. In the Locking tab you set the number of seconds users have to reestablish locks after a server reboot or you can manually release locks on specified clients.

UNIX and Windows 2000 servers differ in how they handle locks. According to SFU Help. "UNIX computers follow advisory locking for all lock requests. This means that the operating system does not enforce lock semantics on a file, and applications that check for the existence of locks can use these locks effectively. However, for NFS implements mandatory locks even for those locking requests that are received via NFS through the server message block (SMB) protocol and to applications accessing the files locally. Mandatory locks are enforced by the operating system.

Client groups are groupings of clients so that you can apply NFS permissions—root access, for example—to the group as a whole rather than to individual systems. If you have a set of computers from which you do system administration and you want all systems to have root access to the NFS server, then you can create a client group, say admin_nodes, and assign access to the NFS export. Click on the Client Groups tab to create client groups and remove them from those groups.

# 11.4.1.3 Exporting Directories (Creating NFS Shares)

To export a directory via NFS on Windows 2000, you create what is called an NFS share. To create an NFS share,

+   1. Open Windows Explorer.
2. In the details pane, right-click on the directory you want to share.
3. Click Sharing.
4. Click NFS Sharing.
5. Click Share this folder and, in the Share name text box, type a share name. See Figure 11–9.