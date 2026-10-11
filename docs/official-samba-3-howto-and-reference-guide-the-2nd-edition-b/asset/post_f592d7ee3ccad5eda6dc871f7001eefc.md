
A Windows group account called “SupportEngrs” can be added by executing the following command:

```
root#  net rpc group add "SupportEngrs" -Uroot%not24get
```

The addition will result in immediate availability of the new group account as validated by executing this command:

```
root#  net rpc group list -Uroot%not24get
Password:
Domain Admins
Domain Users
Domain Guests
Print Operators
Backup Operators
Replicator
Domain Computers
Engineers
SupportEngrs
```

The following demonstrates that the POSIX (UNIX/Linux system account) group has been created by calling the *add group script = /opt/IDEALX/sbin/smbldap-groupadd -p “%g” interface script*:

```
root#  getent group
..
Domain Admins:x:512:root
Domain Users:x:513:ght,ict,ajt,met
Domain Guests:x:514:
Print Operators:x:550:
Backup Operators:x:551:
Replicator:x:552:
Domain Computers:x:553:
Engineers:x:1002:ght
SupportEngrs:x:1003:
```

The following demonstrates that the use of the *net* command to add a group account results in immediate mapping of the POSIX group that has been created to the Windows group account as shown here:

```
root#  net groupmap list
Domain Admins (S-1-5-21-72630-4128915-11681869-512) -> Domain Admins
Domain Users (S-1-5-21-72630-4128915-11681869-513) -> Domain Users
Domain Guests (S-1-5-21-72630-4128915-11681869-514) -> Domain Guests
Print Operators (S-1-5-21-72630-4128915-11681869-550) -> Print Operators
Backup Operators (S-1-5-21-72630-4128915-11681869-551) -> Backup Operators
Replicator (S-1-5-21-72630-4128915-11681869-552) -> Replicator
Domain Computers (S-1-5-21-72630-4128915-11681869-553) -> Domain Computers
Engineers (S-1-5-21-72630-4128915-11681869-3005) -> Engineers
SupportEngrs (S-1-5-21-72630-4128915-11681869-3007) -> SupportEngrs
```

### 12.3.1.2 Mapping Windows Groups to UNIX Groups

Windows groups must be mapped to UNIX system (POSIX) groups so that file system access controls can be asserted in a manner that is consistent with the methods appropriate to the operating system that is hosting the Samba server.

All file system (file and directory) access controls, within the file system of a UNIX/Linux server that is hosting a Samba server, are implemented using a UID/GID identity tuple. Samba does not in any way override or replace UNIX file system semantics. Thus it is necessary that all Windows networking operations that access the file system provide a mechanism that maps a Windows user to a particular UNIX/Linux group account. The user account must also map to a locally known UID. Note that the **net** command does not call any RPC-functions here but directly accesses the passwd.

Samba depends on default mappings for the Domain Admins, Domain Users, and Domain Guests global groups. Additional groups may be added as shown in the examples just given. There are times when it is necessary to map an existing UNIX group account to a Windows group. This operation, in effect, creates a Windows group account as a consequence of creation of the mapping.

The operations that are permitted include: **add**, **modify**, and **delete**. An example of each operation is shown here.

An existing UNIX group may be mapped to an existing Windows group by this example:

```
root# net groupmap modify ntgroup="Domain Users" unixgroup=users
```

An existing UNIX group may be mapped to a new Windows group as shown here:

```
root# net groupmap add ntgroup="EliteEngrs" unixgroup=Engineers type=d
```

```
root#  net groupmap add ntgroup=EngineDrivers unixgroup=Engineers type=d
```

The deletion and addition operations affected only the logical entities known as Windows groups, or domain groups. These operations are inert to UNIX system groups, meaning that they neither delete nor create UNIX system groups. The mapping of a UNIX group to a Windows group makes the UNIX group available as Windows groups so that files and folders on domain member clients (workstations and servers) can be given domain-wide access controls for domain users and groups.

Two types of Windows groups can be created: domain (global) and local. In the previous examples the Windows groups created were of type domain or global. The following command will create a Windows group of type local.

```
root#  net groupmap add ntgroup=Pixies unixgroup=pixies type=l
```

Supported mapping types are 'd' (domain global) and 'l' (domain local), a domain local group in Samba is treated as local to the individual Samba server. Local groups can be used with Samba to enable multiple nested group support.

### 12.3.1.3 Deleting a Group Account

A group account may be deleted by executing the following command:

```
root#  net rpc group delete SupportEngineers -Uroot%not24get
```

Validation of the deletion is advisable. The same commands may be executed as shown above.

### 12.3.1.4 Rename Group Accounts

> **NOTE**
> 
> This command is not documented in the man pages; it is implemented in the source code, but it does not work at this time. The example given documents, from the source code, how it should work. Watch the release notes of a future release to see when this may have been fixed.

Sometimes it is necessary to rename a group account. Good administrators know how painful some managers' demands can be if this simple request is ignored. The following command demonstrates how the Windows group “SupportEngrs” can be renamed to “CustomerSupport”:

```
root# net rpc group rename SupportEngrs \
CustomerSupport -Uroot%not24get
```

## 12.3.2 Manipulating Group Memberships

Three operations can be performed regarding group membership. It is possible to:
- (1) add Windows users to a Windows group,
- (2) delete Windows users from Windows groups, and
- (3) list the Windows users that are members of a Windows group.

To avoid confusion, it makes sense to check group membership before attempting to make any changes. The getent group will list UNIX/Linux group membership. UNIX/Linux group members are seen also as members of a Windows group that has been mapped using the net groupmap command (see Chapter 11, “Group Mapping: MS Windows and UNIX”). The following list of UNIX/Linux group membership shows that the user ajt is a member of the UNIX/Linux group Engineers.

```
root# getent group
.
Domain Admins:x:512:root
Domain Users:x:513:jht,ict,ajt,met,vlendecke
Domain Guests:x:514:
Print Operators:x:550:
Backup Operators:x:551:
Replicator:x:552:
Domain Computers:x:553:
Engineers:x:1000:jht,ajt
```

The UNIX/Linux groups have been mapped to Windows groups, as is shown here:

```
root# net groupmap list
Domain Admins (S-1-5-21-72630-412605-116429-512) -> Domain Admins
Domain Users (S-1-5-21-72630-412605-116429-513) -> Domain Users
Domain Guests (S-1-5-21-72630-412605-116429-514) -> Domain Guests
Print Operators (S-1-5-21-72630-412605-116429-550) -> Print Operators
Backup Operators (S-1-5-21-72630-412605-116429-551) -> Backup Operators
Replicator (S-1-5-21-72630-412605-116429-552) -> Replicator
Domain Computers (S-1-5-21-72630-412605-116429-553) -> Domain Computers
Engineers (S-1-5-21-72630-412605-116429-3001) -> Engineers
```

Given that the user ajt is already a member of the UNIX/Linux group and, via the group mapping, a member of the Windows group, an attempt to add this account again should fail. This is demonstrated here:

```
root#  net rpc group addmem "MIDEARTH\Engineers" ajt -Uroot%not24get
Could not add ajt to MIDEARTH\Engineers: NT_STATUS_MEMBER_IN_GROUP
```

This shows that the group mapping between UNIX/Linux groups and Windows groups is effective and transparent.

To permit the user ajt to be added using the **net rpc group** utility, this account must first be removed. The removal and confirmation of its effect is shown here:

```
root#  net rpc group delmem "MIDEARTH\Engineers" ajt -Uroot%not24get
root#  getent group Engineers
Engineers:x:1000:ajt
root#  net rpc group members Engineers -Uroot%not24get
MIDEARTH\ajt
```

In this example both at the UNIX/Linux system level, the group no longer has the ajt as a member. The above also shows this to be the case for Windows group membership.

The account is now added again, using the **net rpc group** utility:

```
root#  net rpc group addmem "MIDEARTH\Engineers" ajt -Uroot%not24get
root#  getent group Engineers
Engineers:x:1000:ajt,ajt
root#  net rpc group members Engineers -Uroot%not24get
MIDEARTH\ajt
MIDEARTH\ajt
```

In this example the members of the Windows Domain Users account are validated using the **net rpc group** utility. Note that the contents of the UNIX/Linux group was shown four paragraphs earlier. The Windows (domain) group membership is shown here:

```
root#  net rpc group members "Domain Users" -Uroot%not24get
MIDEARTH\jht
MIDEARTH\lct
MIDEARTH\ajt
MIDEARTH\met
MIDEARTH\vlendecke
```

This express example shows that Windows group names are treated by Samba (as with MS Windows) in a case-insensitive manner:
