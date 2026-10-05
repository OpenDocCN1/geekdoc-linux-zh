
[content]
## 4.2 Integrating with existing network services

In this section, we describe how to plan for integrating Linux clients in an existing network. We specifically look at how to incorporate Linux clients in a predominantly Microsoft Windows-based network.

### 4.2.1 Setting the environment

Usually a Linux client will not be the first Linux machine added in an environment. Instead, back-end servers are typically the first machines that are migrated to Linux. This means that most descriptions of how to incorporate Linux clients in an existing network will describe the servers as being Samba servers running on Linux. Since this book is focused on client migration only, we decided to consider the scenario where Linux client migration is occurring in an environment where back-end servers have not yet merged.

A Linux client migration project could occur within any of the following environments:

- *NT4 domain with Microsoft Windows NT 4 PDC (and possibly BDCs)*
- Active Directory (AD) domain with Microsoft Windows 2000 or 2003 servers
- NT4 domain with Linux running Samba PDC and BDCs
- Other non-Microsoft Windows domain-based environment

The majority of environments will be the second option, because the first is becoming less common now that NT4 is end-of-life. The third option is becoming more widespread, and most descriptions of client migration already assume the server-end to be migrated to a Samba domain.

In this book, we concentrate on the first two types of environments (that is, a pure Windows environment) for two reasons:

- *Most domains still fit this model.*
- There are already a lot of descriptions about how to put Linux clients in a Samba domain.

**Planning tip:** If a server-side upgrade of the domain to either AD or Samba is already planned, take this into account in the client migration planning. Try to avoid integrating twice.

Within the Linux community, the most widely used tool for integrating UNIX clients with Windows is Samba. Samba originates from being a successful application that provides network services based on the Server Message Block (SMB) protocol. This is the same protocol used by Microsoft Windows to provide client/server networking services for file and printer sharing. Thus, Linux systems

- When using the winbind separator, this can impact most applications being used on the client.

## The winbind separator

Using winbind will lead to a choice for what is used as the winbind-separator. This is the character that will separate the domain name from the username in the Linux username. For example, AD6380+Administrator is the Linux username of the user Administrator in domain AD6380 when the winbind-separator is a plus (+). The impact of the chosen character has to be studied in all applications and network services used. Using the plus (+) character for separation generally is the best choice for Linux shells and applications.

**Planning tip:** Plan and test winbind and the winbind-separator extensively to validate the setting prior to migrating clients.

## LDAP connect to changed Active Directory

Advantages:

- Mapping users to uid and gid is done within the AD, that is, centrally.
- LDAP is a general protocol to connect to AD.

Disadvantages:

- The AD schema needs to be changed.

Using LDAP means that it might be necessary to change the Active Directory schema to include UNIX-like information such as a uid and gid for users and groups. Microsoft's Service for UNIX can be used to do this.

> **Planning tip:** When planning to use LDAP with Active Directory to authenticate, check whether it is possible to extend the Active Directory schema in your organization.

## LDAP connect to directory synchronized with Active Directory

Advantages:

- Mapping users to uid and gid is done within a central directory.
- LDAP is a general protocol to connect to directories.

Disadvantages:

- The two different directories have to be synchronized.

Synchronizing two directories, each containing different objects with partially different definitions, is not a trivial exercise. This is one of the reasons that this method is not discussed in Chapter 9, "Integration how-tos" on page 195.

Choosing to create users locally on the client means extra overhead. In this case when a user is added to the domain, the user ID has to be added to any of the Linux clients that the user will be to connect with that domain. Even though this process could be automated, it is really necessary when using winbind.

In the case of authenticating natively with an Active Directory domain, Kerberos has to be configured as well as Samba.

In summary, the applications that are going to enable us to authenticate with a Windows domain are Samba, Kerberos, winbind, and LDAP.

### 4.2.3 File sharing using domain shares

Let us assume that some Linux clients are joining a domain and the majority of clients will still be Windows clients. In this scenario, the best way to share files is through Windows shares.

Mount shares on a Linux client using the correct mount command (smbmount mount -t cifs) gives the user access to file systems on the Linux client, in a way that is much like any other file system they are using to. However, if the share is not open for everybody, a username and password combination is needed, just like under Windows. When mounting a share manually, the login information can be input without problem. However, this might lead to several other problems:

- Manually mounting shares using the mount command might not be an acceptable practice for all users. Users are not used to having to mount shares manually, because under Windows this is done automatically when logging on.

- A way must be enable automatic mounting on login just like on Windows. In Linux, automatic mounting of SMB shares can be accomplished using entries in the /etc/fstab file.

A simple solution would be to mount shares in a login profile. However, this needs a password, and the user is used to shares supplied upon logon. A Pluggable Authentication Module (PAM) exists to enable automatic mounting at logon, Since this module is not completely yet, care has to be include this. Currently, it is the preferred way to incorporate some sort of single sign-on-like functionality, such as Windows, so that all the shares are mounted automatically on login to the Linux client. When planning for this, extra time should be included to test the pam-mount module on the Linux client. When it works, it is a very powerful method of mounting shares.

**Planning tip:** Test and plan use of pam-mount extensively.

## Home directories and shares

During planning, it might be very tempting to push user directories on Linux clients to Windows shares. This will enable a “inner” client.

Putting the user's home directory on a share would indeed enable logging on to any client and have the same home directory. Using a graphical logon, this would mean getting the same desktop and environment on any client.

However, care has to be taken. Some session managers (most notably KDE) need to create symbolic links or sockets in the user's home directory as part of normal operation. One of the shortcomings of the SMB file system is that symbolic links or sockets cannot be created in such a file system. This means that any KDE-based application would have problems when running on the desktop machine in a scenario where home directories are remotely mounted on shares.

**Planning tip:** A strategy using remote file shares for mounting of directories which will need to be carefully tested.

### 4.2.4 Printing services in the domain

Of course, it is possible to add printers directly to Linux clients. But this creates extra administrative overhead in a scenario where you are integrating Linux clients into an existing Windows domain that provides printing services already. Since almost all Linux distributions now include the Common UNIX Printing System (CUPS), it is possible to use CUPS in conjunction with Samba on the client to enable printing to the existing domain printers.

If you plan to use CUPS on the Linux clients to print to printers, some issues have to be taken into account:

- Is CUPS and Samba integration handled correctly?
- Do the printers need authentication? Domain passwords for shared printer access be.
- What are the advantages of using print versus direct printing to the printers network interface?
- Are drivers available for CUPS for each printer model in use?
[/content]
