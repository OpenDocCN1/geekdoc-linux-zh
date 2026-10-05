# Global Settings

```
############################ [global]

# workgroup = NT-Domain-Name or Workgroup-Name, eg: REDHAT4
workgroup = BOOK

# Use password server option only with security = server or domain
password server = w2kserv
```

Once you have configured /etc/opt/cifsclient/pam/smb.conf, you then change parameters in /etc/pam.conf. For each application, you must specify the /usr/lib/security/libpam_ntlm.1 authentication mode. On one of my systems, for example, I configured PAM to use NTLM for CDE login (dtlogin), CDE actions (dtaction), and password management. Furthermore, my /etc/pam.conf looks like the following:

```
#
# PAM Configuration
#
# Account Management
#
dtaction account required /usr/lib/security/libpam_ntlm.1
dtlogin account required /usr/lib/security/libpam_ntlm.1
ftp account required /usr/lib/security/libpam_unix.1
login account required /usr/lib/security/libpam_unix.1
 account required /usr/lib/security/libpam_unix.1
OTHER account required /usr/lib/security/libpam_unix.1
#
# Authentication Management
#
dtaction auth required /usr/lib/security/libpam_ntlm.1
dtlogin auth required /usr/lib/security/libpam_ntlm.1
ftp auth required /usr/lib/security/libpam_unix.1
login auth required /usr/lib/security/libpam_unix.1
suth auth required /usr/lib/security/libpam_unix.1
OTHER auth required /usr/lib/security/libpam_unix.1
#
# Password Management
#
dtaction password required /usr/lib/security/libpam_ntlm.1
dtlogin password required /usr/lib/security/libpam_ntlm.1
login password required /usr/lib/security/libpam_unix.1
passwd password required /usr/lib/security/libpam_ntlm.1
OTHER password required /usr/lib/security/libpam_unix.1
#
# Session Management
#
dtaction session required /usr/lib/security/libpam_ntlm.1
dtlogin session required /usr/lib/security/libpam_ntlm.1
login session required /usr/lib/security/libpam_unix.1
OTHER session required /usr/lib/security/libpam_unix.1
```