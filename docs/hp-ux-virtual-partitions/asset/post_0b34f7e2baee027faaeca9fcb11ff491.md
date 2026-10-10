
though from an organizational standpoint, they are in different groups.

Before I cover the groups in general, let’s look at a file belonging to a user and the way access is defined for a file:

```
$ ls -l
-rwxr-x---x    1    marty     users          120    Jul 26    10:20    sort
```

For every file on the system, HP-UX supports three classes of access:

- User access (u). Access is granted to the owner of the file
- Group access (g). Access granted to members of the same group as the owner of the file
- Other access (o). Access granted to everyone else

These access rights are defined by the position of r (read), write (w), and execute (x) when the long listing command is issued. For the long listing (ls -l) above, you see the permissions in Table 6-1.

### TABLE 6-1 Long Listing Permissions

|  | Access | User Access | Group Access | Other |
|---|---|---|---|---|
| Read | r | r | - | - |
| Write | w | - | - | - |
| Execute | x | x | x | x |

You can see that access rights are arranged in groups of three. Three groups of permissions exist with three access levels each. The owner, in this case, marty, is allowed read, write, and execute permissions on the file. Anyone in the group users is permitted read and execute access to the file. Others are permitted only execute access to the file.

These permissions are important to consider as you arrange your users into groups. If several users require access to the same files, then you will want to put those users in the same group. The trade-off here is that you can give all users within a group rwx access to files, but then you run the risk of several users editing a file without other users knowing it, thereby causing confusion. On the other hand, you can make several copies of a file so that each user has his or her personal copy, but then you have multiple versions of a file. If possible, assign users to groups based on their work.

When you run SAM and specify the groups to which each user belongs, the file *etc/group* is updated. The *etc/group* file contains the group name, an encrypted password (which is rarely used), a group ID, and a list of users in the group. Here is an example of an *etc/group* file:

```
root::0:root
other::1:root, hpdh
bin::2:root,bin
sys::3:root,uucp
adm::4:root,adm
daemon::5:root,daemon
mail::6:root
lp::7:root,lp
tty::10:
uucp::11:uuucp
military::25:jhunt,tdolan,vdallesandro
commercial::30:ccascone,jperwinc,devers
nogroup::*:-2:
```

This *etc/group* file shows two different groups of users. Although all users run the same application, a desktop publishing tool, some work on documents of "commercial" products while others work on only "military" documents. It made sense for the system administrator to create two groups, one for commercial document preparation and the other for military document preparation. All members of a group know what documents are current and respect one another's work and its importance. You will have few problems among group members who know what the other members are doing and you will find that these members don't delete files that shouldn't be deleted. If you put all users into one group, however, you may find that you spend more time restoring files, because users in this broader group don't find files that are owned by other members of their group to be important. Users can change group with the **newgrp** command.

## NIS for Managing Users

One of the most popular ways to manage user-related information in a distributed environment is the Network Information System (NIS). NIS provides a method for multiple systems to share a centralized database of password, group, and other optional databases such as services and/or hosts. By doing so, the administration of user accounts is simplified for both end-users and system administrators. You will also often hear NIS referred to as “Yellow Pages” or “YP”; in fact, most of the NIS commands begin with the letters “yp”.

NIS and other such technologies are required only in a distributed environment where users have to be managed on many systems. This is because changes in information, such as adding and removing users, must be disseminated to many systems. This is normally not required in a centralized environment, where only a small number of copies of such information must be maintained.

NIS on HP-UX is interoperable with Solaris and Sun-licensed NIS implementations, including Linux. Like most of these implementations, HP’s NIS is not implemented in C2 or Trusted System mode. Additionally, Microsoft-based operating systems such as Windows do not use or interoperate with NIS.

### What Does NIS Manage?

NIS can manage many different databases. We'll focus on the user password and group information. Table 6-2 is a list of some of the databases NIS can manage:

| FILENAME | INFORMATION CONTAINED IN FILE |
|---|---|
| /etc/passwd | Usernames, user IDs, primary groups, and encrypted passwords. |
| /etc/group | User group memberships. |
| /etc/hosts | Hostnames and IP addresses. |
| /etc/services | Network port numbers and service names. |
| /etc/aliases | Aliases and mailing lists for the mail system. |
| /etc/netgroup | Netgroup definitions. |
| /etc/rpc | Remote procedure call program numbers. |
| /etc/protocols | Network protocol names and numbers. The following are optional for HP, but not used by HP-UX NIS clients. |
| /etc/bootparms | Information about diskless nodes. |
| /etc/ethers | Ethernet numbers (MAC addresses). |
| /etc/netmasks | Network masks. |

NIS also calls each of these databases a *map*. These are called maps because NIS allows you to map a key, such as a username, to a value field, such as the user's **passwd** entry from the **passwd** map on the NIS Master Server.

### How Do I Plan For NIS?

NIS requires one NIS Master Server and typically at least one NIS Slave Server per IP subnet. A NIS Master or Slave Server answers requests from NIS clients typically seeking user password information when a user login occurs. NIS is designed in a "top-down" or hierarchical manner, with all changes being made through the NIS Master Server. When a change is made to the NIS Master, the changes can be made visible to the NIS Slaves by "pushing" the updated database to the Slaves. Generally, an NIS server should satisfy the demands of 25 to 50 NIS clients. NIS Masters and Slaves are typically also NIS clients.

On the NIS Master server, you need to decide where you want to keep the NIS database “source” files. Most typically, the /etc files are used on the NIS Master for all databases except passwords, which are generally put into an “alternate” or “private” password file such as /etc/passwd.nis. Put only the user password database there and not the “system” users, such as root, sys, bin and so on. The “system” users should always be put in /etc/passwd on any NIS server or client.

NIS will provide a small additional network and system load on an NIS Slave and Master server. Most typically, this extra load is encountered when updating a map or database and pushing the changes to the Slave servers.

The design of NIS requires that you first configure the NIS Master Server, then the NIS Slave Servers, and finally, the NIS clients.

### How Do I Configure an NIS Master Or Slave Server?

You can configure a NIS Master and Slave Server either by using SAM or by performing the process manually. If you use SAM to perform this process most of the work will take place for you in the background. You enter the pertinent information and SAM performs the configuration. You perform the steps in the manual procedure. There are many good documents that can help you in this configuration, including HP's *Installing and Administering NFS Services* manual. This manual covers configuring Master and Slave Servers and can be obtained from www.dcs.hp.com. HP support likes when you follow these step-by-step procedures so that should you encounter a problem, your execution of the steps can be reviewed.

To configure with SAM, select *Networking/Communications*, then NIS. You will first be prompted to specify the NIS domain name. After that, you can proceed to the *Enable NIS Master Server* or *Enable NIS Slave Server* menus.
