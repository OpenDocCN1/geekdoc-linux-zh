
In smb.conf, the global settings, which define the overall attributes of a server, follow the first set of comments, including SELinux-related comments covered earlier. The [global] section starts with the following two lines:

```
################ Global Settings ################
[global]
```

Now examine the global settings that follow. First, if you see the line

```
# -authconfig--start-line--
```

this means the configuration file has been modified by the authconfig or the system-config-authentication tool.

## Network-Related Options

Scroll down to the subsection entitled

```
# ---------------- Network Related Options ----------------
```

(In early releases of RHEL 6, the word “Network” is actually misspelled as “Netwok.”) With that in mind, look at each of the directives in this part of the Global Settings section. Despite the name, the workgroup variable specifies the name of a workgroup or more commonly, a domain. But since peer-to-peer workgroups were developed first, the default Samba workgroup is WORKGROUP, which happens to be the old name of the default peer-to-peer workgroup. It’s now set to the default workgroup for Microsoft Windows 7:

```
workgroup = MYGROUP
```

The server string directive that follows becomes the comment shown with the NetBIOS name of the system in the visible browse list, where Samba substitutes the version number for the %v variable:

```
server string = Samba Server Version %v
```

It’s a good idea to add a NetBIOS name for the local system to this file. While limited to 15 characters, it can be the same hostname used for the system. This becomes what other clients see in network browse lists such as those shown from a Microsoft net view command or a regular Linux smbclient command.

```
; netbios name = MYSERVER
```

If the local system is connected to more than one network, you can specify them with the interfaces directive, as shown here. Of course, the devices and network addresses should be changed appropriately.

```
; interfaces = lo eth0 192.168.12.2/24 192.168.13.2/24
```

If you activate the hosts allow directive, that action can limit access to the specified network(s). The following default would limit access to the networks with the 192.168.12.0 and 192.168.13.0 network IP addresses, as well as the local computer (127.):

```
; hosts allow = 127. 192.168.12. 192.168.13.
```

It's possible to configure a hosts deny directive in a similar fashion. With such directives, you can set up host-based security for Samba. In the global section, such security would apply server-wide. You can also use the hosts allow and hosts deny directives in the definitions for individual shared directories, as described later in this chapter.

## Logging Options

The next section sets up logging options, as indicated by the following label:

```
#---------- Logging Options ----------
```

The log file directive as shown sets up separate log files for every machine that connects to this Samba server, based on its machine name (%m). By default, the log file is limited to 50KB. As suggested by the comment, log files that exceed the given size are rotated. If logs exceed that size, you'll still see them in the /var/log/samba directory with the .old extension.

```
# logs split per machine
log file = /var/log/samba/%m.log
# max 50KB per log file, then rotate
max log size = 50
```

## Standalone Server Options

The following section sets up security options, based on configuration as a standalone server:

```
#---------- Standalone Server Options ----------
```

The security directive may be a bit confusing. The standard value of the directive, as shown here, means that connections check the local password database. It is appropriate when configuring this computer as a Domain Controller (DC), specifically a Primary Domain Controller (PDC).

```
security = user
```

Alternatively, to configure this computer as a member server on a domain, use a password database from a DC. Strangely enough, in that case, you would substitute the following command:

```
security = domain
```

![](img/9139201cfcaf4292284a0eed074928e5_833_0.png)

**_To set up a Linux system as a workstation that happens to share directories on a Microsoft domain, you'll need to set up the computer as a member server on that domain._**

To configure a system as a member server on an Active Directory network, substitute the following command:

```
security = ads
```

Alternatively, to use a database from another computer that is not a DC, you'd substitute the following command:

```
security = server
```

Finally, to configure a system on a peer-to-peer workgroup that does not require usernames, substitute the following command:

```
security = share
```

To summarize, there are five basic authentication options: **share**, **user**, **server**, **domain**, and **ads**.

Now, refocus this directive on the authentication database. The default is **security = user**; in this case, make sure the Samba usernames and passwords that you create match those on individual Windows NT/2000/XP/Vista systems on the network. If the database is local, it could be either

```
passdb backend = smbpasswd
```

or

```
passdb backend = tdbsam
```

The smbpasswd database is local, stored in the local /etc/samba directory. The tdb sam option, short for the Trivial Database Security Accounts Manager, sets up a local account database in the /var/lib/samba directory.

Alternatively, for a remote database such as LDAP, you could activate the following directive. If the LDAP server is located on a remote system, that Uniform Resource Identifier (URI) address can be included here.

```
passdb backend = ldapsam
```

If you've set up security = server or security = domain, you'll also want to activate the following directive with the name or IP address of the password server. Alternatively, you could replace <NT-Server-Name> with a * to have Samba search for the password server.

```
; password server = <NT-Server-Name>
```

If you've set up security = ads, you'll also want to activate the following directive to specify the Active Directory (AD) realm, substituting the actual AD realm for MY_REALM:

```
; realm = MY_REALM
```

## Domain Controller Options

The following section supports the configuration of a system as a domain controller, starting with the following comment:

```
#---------- Domain Controller Options ----------
```

Additional configuration is required for a Samba server configured as a domain controller. In brief, these options specify the role of the system as the domain master, as the system that receives requests for logins to the domain:
; domain master = yes
; domain logins = yes
The next command set up Microsoft command line batch files by computer and user. The command afterward stores Microsoft user profiles on the local Samba server. That means these commands can't be tested on the Red Hat exams unless you have access to a Microsoft Windows computer. Since I can't tell what's on the Red Hat exams, I can only suggest that Red Hat might not want separate Microsoft Windows computers available during their exams. Of course, Microsoft Windows guest VMs are included in the description for the Red Hat Enterprise Virtualization course.

```
# the login script name depends on the machine name
; logon script = %m.bat
# the login script name depends on the unix user used
; logon script = %U.bat
; logon path = \\%L\Profiles\%U
```

The remaining commands are fairly self-explanatory, as scripts that add and delete users, groups, and machine accounts.

```
; add user script = /usr/sbin/useradd %u -n -g users
; add group script = /usr/sbin/groupadd %g
; add machine script = /usr/sbin/adduser -n -c \
"Workstation (%u)" -M -d /nohome -s /bin/false %u
; delete user script = /usr/sbin/userdel %u
; delete user from group script = /usr/sbin/userdel %u %g
; delete group script = /usr/sbin/groupdel %g
```

## Browse Control Options

The following section controls whether and how a system may be configured as a browse master, which maintains a list of resources on the network. Related directives start with the following comment:

```
#---------- Browser Control Options ------------
```

Unless a Samba server is specifically designated as a local browse master,

```
; local master = no
```

Samba participates in browser elections like any other Microsoft Windows computer, using the specified os level.

```
; os level = 33
```

Alternatively, if a Domain Controller isn't already elected as a browse master, you can make it easier for the local computer to win the browser election, with the preferred master command:

```
; preferred master = yes
```
