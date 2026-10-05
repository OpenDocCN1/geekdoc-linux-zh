# 8.2.3 Pluggable Authentication Modules

HP-UX 11 supports Pluggable Authentication Modules (PAM). These modules make it possible to use mechanisms other than /etc/passwd or NIS to authenticate users. Other authentication methods include NTLM, Kerberos, and the Distributed Computing Environment (DCE). You configure PAM by editing the /etc/pam.conf file for one or more of four services:

+   * Authentication—Used to verify the identity of a user and to set the user-specific credentials.
* Account management—Used to determine whether the current user's account (not password) is valid. This includes checking for password and account expiration, as well as verifying access hour restrictions.
* Session management—To set up and terminate login sessions.
* Password management—To change a user's authentication token or password.

In /etc/pam.conf you specify what happens when you invoke a particular application for each of these services. As an example, pam.conf may look like the following:

```
#
# PAM Configuration
# Account Management
#
dtaction account required /usr/lib/security/libpam_unix.1
dtlogin account required /usr/lib/security/libpam_unix.1
ftp account required /usr/lib/security/libpam_unix.1
login account required /usr/lib/security/libpam_unix.1
su account required /usr/lib/security/libpam_unix.1
OTHER account required /usr/lib/security/libpam_unix.1
#
# Authentication Management
dtaction auth required /usr/lib/security/libpam_unix.1
dtlogin auth required /usr/lib/security/libpam_unix.1
ftp auth required /usr/lib/security/libpam_unix.1
login auth required /usr/lib/security/libpam_unix.1
su auth required /usr/lib/security/libpam_unix.1
OTHER auth required /usr/lib/security/libpam_unix.1
#
# Password Management
dtaction password required /usr/lib/security/libpam_unix.1
dtlogin password required /usr/lib/security/libpam_unix.1
login password required /usr/lib/security/libpam_unix.1
passwd password required /usr/lib/security/libpam_unix.1
OTHER password required /usr/lib/security/libpam_unix.1
```