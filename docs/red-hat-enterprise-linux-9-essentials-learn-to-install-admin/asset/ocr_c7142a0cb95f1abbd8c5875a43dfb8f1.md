# Sharing Files between RHEL 9 and Windows Systems with Samba

```
comment = Example Samba share
path = /sampleshare
browseable = Yes
public = yes
writable = yes
```

To restrict access to specific users, the “valid users” property may be used, for example:

```
valid users = demo, bobyoung, marcewing
```

# 19.5.3 Removing Unnecessary Shares

The smb.conf file is pre-configured with sections for sharing printers and the home folders of the users on the system. If these resources do not need to be shared, the corresponding sections can be commented out so that Samba ignores them. In the following example, the [homes] section has been commented out:

```
.
#
#[homes]
#      comment = Home Directories
#      valid users = %S, %D%w%S
#      browseable = No
#      read only = No
#      inherit acls = Yes
.
.
```

# 19.6 Configuring SELinux for Samba

SELinux is a system integrated by default into the Linux kernel on all RHEL 9 systems, providing an extra layer of security and protection to the operating system and user files.

Traditionally, Linux security has been based on allowing users to decide who has access to their files and other resources they own. Consider, for example, a file located in the home directory of, and owned by, a particular user. That user can control the access permissions of that file in terms of whether other users on the system can read and write to or, in the case of a script or binary, execute the file. This type of security is called discretionary access control since resource access is left to the user’s discretion.

With SELinux, however, access is controlled by the system administrator and cannot be overridden by the user. This is called mandatory access control and is defined by the administrator using the SELinux policy. To continue the previous example, the owner of a file can only perform tasks on that file if the SELinux policy, defined either by default by the system or by the administrator, permits it.

The current status of SELinux on a RHEL 9 system may be identified using the sestatus tool as follows:

```
SELinux status:               enabled
```