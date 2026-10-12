```
printcap name = /etc/printcap
load printers = yes
```

```
# It should not be necessary to spell out the print system type unless
# yours is non-standard. Currently supported print systems include:
# bsd, sysv, plp, lprng, aix, hpux, qnx
; printing = bsd
```

The next entry in the smb.conf file is required if you want to specify a guest account for anonymous access to services on your Samba server. This is not a requirement, and by default, guest access is permitted via the nobody account.

```
# Uncomment this if you want a guest account, you must add this to
# /etc/passwd, otherwise the user 'nobody' is used
; guest account = pcguest
```

It is occasionally necessary to troubleshoot problems with connections by Windows clients. The following two entries specify the number of characters to compare when matching user names and passwords. The comparisons for this number of characters are case insensitive. These entries should only be uncommented while actively debugging problems.

```
# Password Level allows matching of _n_ characters of the password for
# all combinations of upper and lower case.
; password level = 8
; username level = 8
```

Passwords are encrypted by default with Windows 95 OSR2 and later, including of course, Windows NT. Prior to this release, passwords are passed as clear text. Encryption of passwords by the Samba server, however, is not enabled by default if using the smb.conf file that comes with Red Hat, as shown in the following lines:

```
# You may wish to use password encryption. Please read
# ENCRYPTION.txt, Win95.txt and WinNT.txt in the Samba documentation.
# Do not enable this option unless you have read those documents
; encrypt passwords = yes
; smb passwd file = /etc/smbpasswd
```

This situation means that you must make a decision on whether to support this feature. You have several options as to how to deal with this situation. Two of these are described below.

```
smbpasswd -a userid
```