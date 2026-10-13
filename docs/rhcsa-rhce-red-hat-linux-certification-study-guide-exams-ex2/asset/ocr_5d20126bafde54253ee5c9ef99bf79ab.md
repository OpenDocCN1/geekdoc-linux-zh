Windows guest VMs are included in the description for the Red Hat Enterprise Virtualization course.

```
```
# the login script name depends on the machine name
; logon script = %m.bat
# the login script name depends on the unix user used
; logon script = %U.bat
; logon path = \\%L\Profiles\%U
```
```

The remaining commands are fairly self-explanatory, as scripts that add and delete users, groups, and machine accounts.

```
```
; add user script = /usr/sbin/useradd %u -n -g users
; add group script = /usr/sbin/groupadd %g
; add machine script = /usr/sbin/adduser -n -c \
"Workstation (%u)" -M -d /nohome -s /bin/false %u
; delete user script = /usr/sbin/userdel %u
; delete user from group script = /usr/sbin/userdel %u %g
; delete group script = /usr/sbin/groupdel %g
```
```

# Browse Control Options

The following section controls whether and how a system may be configured as a browse master, which maintains a list of resources on the network. Related directives start with the following comment:

```
```
#---------- Browser Control Options ------------
```
```

Unless a Samba server is specifically designated as a local browse master,

```
```
; local master = no
```
```

Samba participates in browser elections like any other Microsoft Windows computer, using the specified os level.

```
```
; os level = 33
```
```

Alternatively, if a Domain Controller isn't already elected as a browse master, you can make it easier for the local computer to win the browser election, with the preferred master command:

```
```
; preferred master = yes
```
```