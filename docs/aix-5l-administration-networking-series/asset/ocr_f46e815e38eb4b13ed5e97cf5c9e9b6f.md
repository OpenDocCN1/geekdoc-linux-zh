# The /etc/security/user File

The /etc/security/user file contains the extended attributes defined for the user. Each user is identified by a user name stanza followed by each attribute and value. A default stanza follows the header comments in the file. Each user entry may override a default attribute by specifying a local value. See the following example:

```
```
default:
admin = false
login = true
su = true
daemon = true
rlogin = true
sugroups = ALL
ttys = ALL
auth1 = SYSTEM
auth2 = NONE
tpath = nosak
umask = 022
expires = 0
stimpy:
login = false
rlogin = false
```
```

# Salting Group and Passwd Files

In large environments, there may be a need to synchronize the user and group space for system and applications across all new installs. This means that the mqm, cics, and kmem groups, as well as the cics and mqm user ID numbers, must be defined before the TXSeries, MQSeries, and freeware.Isolfrte applications are installed. When the applications are installed, they will create their user and group with different results if they do not already exist. The solution is to create a minimum installed image from the AIX 5L base install CD and then add, or salt, the entire list of future group and user IDs that your enterprise may ever need. The image can be salted with your own script that adds groups and users with native commands, or the system can pull over the master files from the control workstation if there are no ID conflicts. Here is a list of some of the files you may want to pull or push from the master repository workstation:

```
```
/etc/passwd
/etc/passwd.nm.idx
/etc/passwd.id.idx
/etc/group
/etc/security/passwd
/etc/security/passwd.idx
```
```