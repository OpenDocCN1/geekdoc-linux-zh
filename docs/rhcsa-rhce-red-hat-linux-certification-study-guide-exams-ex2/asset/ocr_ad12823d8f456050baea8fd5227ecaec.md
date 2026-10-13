computers. Make your own judgment on whether this section might apply during an RHCE exam.

```
# Un-comment the following to provide a specific roving profile
# share; the default is to use the user's home directory
;[Profiles]
; path = /var/lib/samba/profiles
; browseable = no
; guest ok = yes
```

# Group Directories

The following stanza, as suggested by the comment, configures the /home/samba directory to be shared by the group named staff. You can configure this common group of users to share this directory. To configure special ownership and permissions for /home/samba, you'll need also to configure appropriate permissions. Both processes are described in Chapter 8.

```
# A publicly accessible directory, but read only, except for
# people in the "staff" group
;[public]
; comment = Public Stuff
; path = /home/samba
; public = yes
; writable = yes
; printable = no
; write list = +staff
```

To set up appropriate permissions on the shared directory, you may also want to include the following directives for creating files and directories:

```
create mask = 0770
directory mask = 2770
```

One difference with Samba is that Microsoft authentication databases do not allow users and groups to have the same names. In addition, the /home/samba directory, along with any files contained in that directory, normally must have the proper SELinux file type, something made possible with the following command:

```
# chcon -R -t samba_share_t /home/samba
```

Of course, you'll want to make sure such a change survives a SELinux relabel, and that can be configured for the noted directory with the following command:

```
# semanage fcontext -a -t samba_share_t /home/samba
```