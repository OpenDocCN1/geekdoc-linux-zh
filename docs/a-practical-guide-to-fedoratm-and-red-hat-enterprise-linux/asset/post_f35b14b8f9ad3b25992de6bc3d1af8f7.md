
# CHAPTER SUMMARY

NFS allows a server to share selected local directory hierarchies with client systems on a heterogeneous network, thereby reducing storage needs and administrative overhead. NFS defines a client/server relationship in which a server provides directory hierarchies that clients can mount.

On the server, the */etc/exports* file lists the directory hierarchies that the system exports. Each line in **exports** specifies a directory hierarchy and the client systems that are allowed to mount it, including options for each client (readonly, read-write, and so on). An `exports -r` command causes NFS to reread this file.

From a client, a `mount` command mounts an exported NFS directory hierarchy. Alternatively, you can put an entry in */etc/fstab* to have the system automatically mount the directory hierarchy when it mounts the local filesystems.

Automatically mounted directory hierarchies help manage large groups of systems containing many servers and directory hierarchies in a consistent way and can help remove server-server dependencies. The `automount` daemon automatically mounts `autofs` directory hierarchies when they are needed and unmounts them when they are no longer needed.

# EXERCISES

- 1. What are three reasons to use NFS?
- 2. Which command would you give to mount on the local system the */home* directory hierarchy that resides on the file server named **plum**? Assume the mounted directory hierarchy will appear as **plum:/home** on the local system. How would you mount the same directory hierarchy if it resided on the fileserver at 192.168.1.1? How would you unmount */home*?
- 3. How would you list the mount points on the remote server named **plum** that the local client named **guava** can mount?
- 4. Which command line lists the currently mounted NFS directory hierarchies?
- 5. What does the */etc/fstab* file do?
- 6. From a server, how would you allow readonly access to /opt for any system in example.com?

# ADVANCED EXERCISES

- 7. When is it a good idea to disable attribute caching?
- 8. Describe the difference between the root_squash and all_squash options in /etc/exports.
- 9. Why does the secure option in /etc/exports not really provide any security?
- 10. Some diskless workstations use NFS as swap space. Why is this approach useful? What is the downside?
- 11. NFS maps users on the client to users on the server. Explain why this mapping is a security risk.
- 12. What does the mount nosuid option do? Why would you want to use this option?

# 23 SAMBA: LINUX AND WINDOWS FILE AND PRINTER SHARING

- **In This Chapter**
  - Introduction to Samba . . . . . . . . . . . . . . . . . 828
  - smbpasswd and pdbedit: Work with Samba Users and Passwords . . . . . . . . . . . . . . . 831
  - Running Samba Clients . . . . . . . . . . . . 832
  - Setting Up a Samba Server . . . . . . . . . . . 836
  - JumpStart: Configuring a Samba Server Using system-config-samba (Fedora) . . . 837
  - smb.conf: Manually Configuring a Samba Server . . . . . . . . . . . . . . . 839
  - Troubleshooting . . . . . . . . . . . . . . . . . . . . 846

### Objectives

After reading this chapter you should be able to:

- ▶ Describe the use, history, and components of Samba
- ▶ List capabilities of the Samba server
- ▶ Use a variety of Samba client tools
- ▶ Describe Samba authentication methods
- ▶ Configure a Samba share for local accounts
- ▶ Troubleshoot Samba connections

Samba is a suite of programs that enables UNIX-like operating systems, including Linux, Solaris, FreeBSD, and Mac OS X, to share files and printers with other operating systems, such as OS/2 and Windows, as both a server and a client.

As a server, Samba shares Linux files and printers with Windows systems. As a client, Samba gives Linux users access to files and printers on Windows systems. Its ability to share files across operating systems makes Samba an ideal tool in a heterogeneous computing environment.

Refer to pages 574 and 576 for information about printing to and from a Windows machine using CUPS and Samba.

# INTRODUCTION TO SAMBA

This chapter starts by providing a list of Samba tools followed by some basic information about Samba. The section on Samba clients explains how to use Samba to work with files and printers on a remote system. The next section describes three ways to configure a Samba server. First, a JumpStart section explains how to use the `system-config-samba` GUI (Fedora only) to set up a Samba server. The next sections cover using a text editor to edit Samba configuration files. The final section, “Troubleshooting” on page 846, offers tips on what to do when Samba does not work properly.

Table 23-1 lists some of the utilities and daemons that make up the Samba suite of programs. See the samba man page for a complete list.

**Table 23-1** Samba utilities and daemons

| Utility or daemon | Function |
| :--- | :--- |
| **net** | This utility has the same syntax as the DOS `net` command and, over time, will eventually replace other Samba utilities such as `smbpasswd`. |
| **nmbd** | The `NetBIOS` (page 1262) nameserver program, run as a daemon by default. Provides NetBIOS over IP naming services for Samba clients. Also provides browsing support for Samba shares on remote systems. |
| `nmblookup` | Queries the `NetBIOS` (page 1262) name; see page 847. |
| `pdbedit` | Maintains the Samba user database (page 831). |
| `smbclient` | Displays shares on a Samba server such as a Windows machine; uses ftp-like commands (page 833). |
| **smbd** | The Samba program, run as a daemon by default. Provides file and print services for Samba and Windows clients. |
| `smbpasswd` | Changes Windows NT password hashes on Samba and Windows NT servers (page 831). |
| `smbstatus` | Displays information about current `smbd` connections. |
| `smbtar` | Backs up and restores data from Samba servers; similar to tar. |
| `smbtree` | Displays a hierarchical diagram of available shares (page 832). |
| `testparm` | Checks the syntax of the `smb.conf` file (page 846). |

# MORE INFORMATION

- **Web** Samba: www.samba.org (mailing lists, documentation, downloads, and more)
- **HOWTO** Unofficial Samba HOWTO: www.oregontechsupport.com/samba.

# NOTES

- **Client firewall** The Samba *clients* normally use UDP ports 137 and 138. If the client is running a firewall or is behind a firewall, you need to open these ports. Give the following commands to open the ports each time the system boots (permanently!) and on the running system; see page 906 for information on *firewall-cmd*.

```bash
# firewall-cmd --add-port=137/udp
# firewall-cmd --permanent --add-port=137/udp
# firewall-cmd --add-port=138/udp
# firewall-cmd --permanent --add-port=138/udp
```

- **Share** Under Samba and Windows, an exported directory hierarchy is called a *share*.
- **Mapping a share** The Samba/Windows term *mapping a share* is equivalent to the Linux term *mounting a directory hierarchy*.
- **Samba** The name *Samba* is derived from *SMB* (page 1273), the protocol that is the native method of file and printer sharing for Windows. Also *CIFS* (next).
- **CIFS** *CIFS* (page 1242) is an Internet filesystem protocol based on *SMB* (previous). The terms *SMB* and *CIFS* are used interchangeably.
- **Printing** Using CUPS to print on a printer connected to a Linux system is easier and can be made more secure than using Samba to print from Windows. For more information refer to “Printing from Windows” on page 574.
- **Troubleshooting** If the server does not work properly, see “Troubleshooting” on page 846.

# SAMBA USERS, USER MAPS, AND PASSWORDS

- **Authentication** For a Windows user to access Samba services on a Linux system, the user must provide a Windows username and a Samba password. In some cases, Windows supplies the username and password for you. Alternatively, you can log in as the user named *guest* (the Anonymous user; next page). It is also possible to authenticate using other methods. For example, Samba can use *LDAP* (page 1257) or *PAM* (page 476) instead of the default password file. Refer to the Samba documentation for more information on authentication methods.
