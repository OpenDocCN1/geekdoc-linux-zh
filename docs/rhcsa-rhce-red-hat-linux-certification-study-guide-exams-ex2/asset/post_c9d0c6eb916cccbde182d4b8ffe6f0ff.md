
## FIGURE 16-2

Firewall configuration written by system-config-firewall
Manual customization of this file is not recommended.

Firewall rules for NFS

```
#filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 2049 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT
-A INPUT -m state --state NEW -m udp -p udp --dport 111 -j ACCEPT
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT
~
"/etc/sysconfig/iptables" 17L, 740C
```

## Make NFS Work with SELinux

Of course, appropriate firewalls are not enough. SELinux is an integral part of the security landscape, with respect to both boolean options and files. First, there are two file types associated with NFS:

- **var_lib_nfs_t** Associated with dynamic files in the /var/lib/nfs directory. Files in this directory are updated as shares are mounted, as files from shared directories are called and locked.
- **nfsd_exec_t** Assigned to system executable files such as **rpc.mountd** and **rpc.nfsd** in the /usr/sbin directory. Closely related are the rpcd_exec_t and gssd_exec_t file types, for services associated with RPCs and communications with Kerberos servers.

In general, you won't have to assign a new file type to a shared NFS directory. So for most administrators, these file types are shown for reference.

So for SELinux, the boolean directives are most important. The options are shown in the Booleans section of the SELinux Administration tool, with the nfs filter, as shown in Figure 16-3. The figure reflects the default configuration; in other words, the global modules are all enabled by default. The following directives are associated with making NFS work with SELinux in targeted mode. While most of these modules were already listed in Chapter 10,

### FIGURE 16-3 NFS-related SELinux boolean options

![](img/9139201cfcaf4292284a0eed074928e5_887_0.png)

they're worth repeating, if only to help those who fear SELinux. The first module is not shown in Figure 16-3. The remaining modules are described in the order shown in the figure.

- **allow_gssd_read_tmp** Supports the reading of temporary directories by the General Security Services daemon, gssd, which helps protect NFS when systems authenticate through Kerberos 5.
- **httpd_use_nfs** Supports access to shared NFS directories by the Apache Web server.
- **cd_record_read_content** Enables access to mounted NFS directories by the cdrecord command.
- **allow_ftpd_use_nfs** Allows the use of shared NFS directories by FTP servers.
- **git_system_use_nfs** Supports access of NFS shares by the git revision control system service.
- **nfs_export_all_ro** Supports read-only access to shared NFS directories.
- **nfs_export_all_rw** Supports read/write access to shared NFS directories.
- **use_nfs_home_dirs** Enables the mounting of /home on a remote NFS server.
- **qemu_use_nfs** Allows access by the quick emulator to NFS-mounted filesystems.
- **allow_nfsd_anon_write** Supports NFS servers when they modify files on public file transfer services.
- **samba_share_nfs** Allows Samba to export NFS-mounted directories.
- **virt_use_nfs** Enables access by VMs to NFS-mounted filesystems.
- **xen_use_nfs** Allows access by the Xen virtual machine monitor to NFS-mounted filesystems.

To set these directives, use the setsebool command. For example, to activate access by an FTP server, in a way that survives a reboot, run the following command:

```
# setsebool -P allow_ftpd_use_nfs 1
```

## Quirks and Limitations of NFS

NFS does have its problems. Any administrator who controls shared NFS directories would be wise to take note of these limitations.

### Statelessness

NFS is a "stateless" protocol. In other words, you don't need to log in separately to access a shared NFS directory. Instead, the NFS client normally contacts rpc.mountd on the server. The rpc.mountd daemon handles mount requests. It checks the request against currently exported filesystems. If the request is valid, rpc.mountd provides an NFS file handle (a "magic cookie"), which is then used for further client/server communication for this share.

The stateless protocol allows the NFS client to wait if the NFS server ever has to be rebooted. The software waits, and waits, and waits. This can cause the NFS client to hang. The client may even have to reboot or even power-cycle the system.

This can also lead to problems with insecure single-user clients. When a file is opened through a share, it may be "locked out" from other users. When an NFS server is rebooted, handling the locked file can be difficult. The security problems can be so severe that NFS communication is blocked even by the default Red Hat Enterprise Linux firewall.

In theory, the recent change to NFS, setting up sync as the default for file transfers, should help address this problem. In theory, locked-out users should not lose any data that they've written with the appropriate commands.

### Absolute and Relative Symbolic Links

If you have any symbolic links on an exported directory, be careful. The client interprets a symbolically linked file from a remotely mounted directory as if it were a local link. Unless the mount point and filesystem structures are identical, the linked file can point to an unexpected location, which may lead to unpredictable consequences.

There are two ways to address this issue. You can take the time to analyze the exported directory, limiting the use of symbolic links. Alternatively, you could use the NFS server-side export option (link_relative) that converts absolute links to relative links; however, this can have counterintuitive results if the client mounts a subdirectory of the exported directory.

### Root Squash

By default, NFS is set up to root_squash, which prevents root users on an NFS client from gaining root access to a share on an NFS server. Specifically, the root user on a client (with a user ID of 0) is mapped to the nfsnobody unprivileged account (if in doubt, check the local /etc/passwd file).

This behavior can be disabled via the no_root_squash server export option in /etc/exports. For exported directories so disabled, remote root users can use their root privileges on the shared NFS directory. While it can be useful, it is also a security risk, especially from crackers who use their own Linux systems to take advantage of those root privileges.

### NFS Hangs

Because NFS is stateless, NFS clients may wait up to several minutes for a server. In some cases, an NFS client may wait indefinitely if a server goes down. During the wait, any process that looks for a file on the mounted NFS share will hang. Once this happens, it is generally difficult or impossible to unmount the offending filesystems. You can do several things to reduce the impact of this problem:

- Take great care to ensure the reliability of NFS servers and the network.
- Avoid mounting many different NFS servers at once. If several computers mount each other's NFS directories, this could cause problems throughout the network.
- Mount infrequently used NFS exports only when needed. NFS clients should unmount these clients after use.
- Set up NFS shares with the sync option, which should at least reduce the incidence of lost files.
- Avoid configuring a mission-critical computer as an NFS client.
- Keep NFS mounted directories out of the search path for users, especially that of root.
- Keep NFS mounted directories out of the root (/) directory; instead, segregate them to a less frequently used filesystem, if possible, on a separate partition.

### Inverse DNS Pointers

An NFS server daemon checks mount requests. First, it looks at the current list of exports, based on /etc/exports. Then it looks up the client's IP address to find its host name. This requires a reverse DNS lookup.

This host name is then finally checked against the list of exports. If NFS can't find a host name, rpc.mountd will deny access to that client. For security reasons, it also adds a "request from unknown host" entry in /var/log/messages.

### File Locking

Multiple NFS clients can be set up to mount the same exported directory from the same server. It's quite possible that people on different computers end up trying to use the same shared file. This is addressed by the file-locking daemon service.

While mandatory locks can now be configured with NFSv4, NFS has historically had serious problems with file locks. If you have an application that depends on file locking over NFS, test it thoroughly before putting it into production.

### Performance Tips

You can do several things to keep NFS running in a stable and reliable manner. As you gain experience with NFS, you might monitor or even experiment with the following factors:
