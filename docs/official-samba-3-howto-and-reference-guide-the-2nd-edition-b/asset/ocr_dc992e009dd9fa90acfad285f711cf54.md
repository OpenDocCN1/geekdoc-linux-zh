PAM provides a mechanism that disconnects these security programs from the underlying authentication/authorization infrastructure. PAM is configured by making appropriate modifications to one file, `/etc/pam.conf` (Solaris), or by editing individual control files that are located in `/etc/pam.d.`

On PAM-enabled UNIX/Linux systems, it is an easy matter to configure the system to use any authentication backend so long as the appropriate dynamically loadable library modules are available for it. The backend may be local to the system or may be centralized on a remote server.

PAM support modules are available for:

`/etc/passwd` There are several PAM modules that interact with this standard UNIX user database. The most common are called `pam_unix.so`, `pam_unix2.so`, `pam_pwb.so` and `pam_userdb.so`.

**Kerberos** The `pam_krb5.so` module allows the use of any Kerberos-compliant server. This tool is used to access MIT Kerberos, Heimdal Kerberos, and potentially Microsoft Active Directory (if enabled).

**LDAP** The `pam_ldap.so` module allows the use of any LDAP v2- or v3-compatible backend server. Commonly used LDAP backend servers include OpenLDAP v2.0 and v2.1, Sun ONE iDirectory server, Novell eDirectory server, and Microsoft Active Directory.

**NetWare Bindery** The `pam_ncp_auth.so` module allows authentication off any bindery-enabled NetWare Core Protocol-based server.

**SMB Password** This module, called `pam_smbpass.so`, allows user authentication of the passdb backend that is configured in the Samba `smb.conf` file.

**SMB Server** The `pam_smb_auth.so` module is the original MS Windows networking authentication tool. This module has been somewhat outdated by the Winbind module.

**Winbind** The `pam_winbind.so` module allows Samba to obtain authentication from any MS Windows domain controller. It can just as easily be used to authenticate users for access to any PAM-enabled application.

**RADIUS** There is a PAM RADIUS (Remote Access Dial-In User Service) authentication module. In most cases, administrators need to locate the source code for this tool and compile and install it themselves. RADIUS protocols are used by many routers and terminal servers.

Of the modules listed, Samba provides the `pam_smbpasswd.so` and the `pam_winbind.so` modules alone.