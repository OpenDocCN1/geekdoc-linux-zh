
# Samba Global Options

> NOTE

> Samba directives include many synonyms. For example, hosts allow is the same as allows hosts. Samba directives also accommodate alternative spellings, such as browse and browseable. If you see one directive in documentation and a similar one in a configuration file, look a little deeper. The directives might mean the same thing.

This section focuses on directives in the main Samba configuration file, smb.conf, in the /etc/samba/ directory. The directives associated with sharing directories were discussed in Chapter 5; this section focuses primarily on the directives in the [global] section of this file. When reading this, be aware there are two different characters; any line that starts with a pound sign (#) or a semicolon (;) is a comment in this file.

Any Linux system configured with Samba can be set up as a server on a Microsoft network. While this is based on the Samba configuration file from Red Enterprise Linux version 5.4, the same directives can be used on any Linux system where the (or later) version of Samba is installed. The following subsections are based on the sections from the sample version of that file.

One thing that may appear different many Samba directives is that they're multiple words. Don't be fooled. Multiple-word directives like server string and user script are a single directive.

# Network-Related Options

Microsoft networks work with computers where directories are shared solely by passwords. As such, Samba used the workgroup directive to specify the name of the noted group of computers. When the latest Microsoft networks evolved into domains, Samba retained the workgroup directive to specify the name of the domain. So depending on the type of network being configured, the value assigned to workgroup can be the name of either a workgroup or a domain.

As shown here, the workgroup directive is normally coupled with the server string and netbios directives. The example shown "Samba Server Version" followed by the version number of the Samba server, as specified by the %y. It's shown as a comment in a Microsoft My Places window or in the output of a Microsoft net view or sambaclient -L command.

```
workgroup = bigdomain
server string = Samba Server Version %y
netbios name = trivialinfo
```

If obscurity is part of your security strategy, consider changing the values of server string and netbios name. The values shown there can carry off the casual hacker. The netbios name directive is associated with the Network Input/Output System (NetBIOS) name, which is associated with the Open Systems Interconnection (OSI) model of networking. If the netbios name is not assigned, the hostname is used.

# Networked Filesystems and Remote Access

The interfaces and hosts allow directive can access the Samba server in two ways. The examples shown here limit the interfaces which Samba listens. The hosts allow directive can be revised to limit access to a domain or individual host.

```
interfaces = eth0 192.168.1.0/24
hosts allow = 127.0.0.1 192.168.1.0/24
```

# Logging Options

It may be helpful to set up logs by different machines. The following directives set up log files by NetBIOS name or IP address. The max log size directive sets a limit on log files in kilobytes.

```
log file = /var/log/samba/%m
max log size = 0
```

# Standalone Server Options

This section is closely related to the next section. Some of the options and directives are mutually exclusive. For example, you should activate only one security directive in this configuration. The two security options described in this section are user and share. For a standalone server, a PDC, or BDC, you'd need to set up the following:

```
security = user
passdb backend = smpasswd
```

The smpasswd options allow administrators to set or change passwords with the smpasswd command. Be aware: The Samba user database is separate from the Linux password database, and is stored in files in /etc/samba/directory. If you use LDAP database, set passdb backend = ldaps. You may consider including a number of other related directives in Table 8-1. The table just lists some of the most important LDAP directives: for example, options associated with logging are not included in the list and some of the directives may be used to map Linux UIDs and group GIDs (IDs) to other authentication databases. If the local system is configured as one server on the local network, the authentication database will be stored on the local system. Depending on how smb.conf is configured, that will be in files either in /etc/samba/ or /etc/samba/private/ directory.

![](img/c060a8c8a0777903dfec4ff61ffa1_254_0.png)

Table 8-1 LDAP-related Samba directives.

| LDAP DIRECTIVE | DESCRIPTION |
| :--- | :--- |
| client ldap sasl wrapping | Allows LDAP traffic to be encrypted by the simple authentication and security layer (SASL); associated the following registry key: HKLM\System\CurrentControlSet\Services\NTDS\Parameters\LDAPServerIntegrity |
| idmap backend | Supports a database association between Microsoft security identifiers (SIDs) and Linux UIDs and GIDs |
| idmap gid | Specifies a range of GIDs to be mapped, not limited to LDAP authentication databases |
| idmap uid | Specifies a range of UIDs to be mapped to Microsoft SIDs; not limited to LDAP authentication databases |
| ldap admin dn | Specifies the distinguished name to contact the LDAP server |
| ldap group suffix | Sets the suffix to be used for LDAP groups, such as ou=Groups |
| ldap machine suffix | Defines the suffix to be used for LDAP systems, such as ou=Computers |
| ldap password sync | Defines whether the Microsoft LDAP database is to be updated when a Samba password is updated |
| ldap suffix | Sets the base entry for the object, such as dc=example,dc=org |
| ldap user suffix | Sets the suffix to be used for LDAP users, such as ou=People |

FYI

One trivial bit is the terms associated with user authentication on Linux and Microsoft systems. Users on Linux systems log in to a computer. Because Samba is the Linux implementation of Microsoft networking, the Samba configuration file configures Microsoft-style user logins.

Thus, the comments in the Samba server configuration file specify “login” and the associated directives use logon.

If you are configuring a PDC, pay attention to the [netlogon] and [profiles] stanzas in the “Shares Definitions” section of the smb.conf configuration file. These stanzas determine how logon information is shared by user.

- domain master—Determines whether the local system forces an election for the domain.
- local master—Determines whether the system puts itself up for election.
- os level—Sets the advertising level for browsing elections; may be set between 0 and 255.
- preferred master—Determines whether the local system forces an election for the local network.

# Name Resolution

Name resolution on Microsoft networks is based on the status of Windows Internet Name Service (WINS) and DNS servers. A WINS server contains a database of NetBIOS names and IP addresses. If the NetBIOS name does not exist, the WINS server defaults to the hostname of the system. The basic directives in this section are straightforward:

- wins support—Enables a WINS server on the local system.
- wins server—Configures a pointer to a running WINS server.
- wins proxy—Redirects WINS requests to a system specified by wins proxy.
- dns proxy—Supports NetBIOS name resolution via DNS.
