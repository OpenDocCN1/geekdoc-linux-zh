**Listing 11-1 Continued**

```
```text
; username level = 0
```

```text
# You may wish to use password encryption. Please read
# ENCRYPTION.txt, Win95.txt and WinNT.txt in the Samba documentation.
# Do not enable this option unless you have read those documents
; encrypt passwords = yes
; smb passwd file = /etc/samba/smbpasswd
```

```text
# The following are needed to allow password changing from Windows to
# update the Linux system password also.

# NOTE: Use these with 'encrypt passwords' and 'smb passwd file' above.
# NOTE2: You do NOT need these to allow workstations to change only
#
#       the encrypted SMB passwords. They allow the Unix password
#
#       to be kept in sync with the SMB password.
; unix password sync = Yes
; passwd program = /usr/bin/passwd %u
; passwd chat = *UNIX*new*password* \n
 *Re*type*new*UNIX*password* \n
 *password*all*authentication*tokens*updated*successfully*
```

```text
# Unix users can map to different SMB User names
# username map = /etc/samba/csumbers
```

```text
# Using the following line enables you to customize your configuration
# on a per machine basis. The %m gets replaced with the netbios name
# of the machine that is connecting
; include = /etc/samba/smb.conf.%m
```

```text
# Most people will find that this option gives better performance.
# See speed.txt and the manual pages for details
   socket options = TCP_NODELAY SO_RCVBUP=8192 SO_SNDBUF=8192
```

```text
# Configure Samba to use multiple interfaces
#
# If you have multiple network interfaces then you must list them
# here. See the man page for details.
```
```