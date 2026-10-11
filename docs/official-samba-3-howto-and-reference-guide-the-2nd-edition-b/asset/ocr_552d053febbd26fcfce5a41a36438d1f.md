# ## SEE ALSO

winbindd(8) and ntlm_auth(1)

# ## 47.20 winbindd

# ### Synopsis

```
winbindd [-F] [-S] [-i] [-Y] [-d <debug_level>] [-s <smb_config_file>]
    [-n]
```

# ## DESCRIPTION

This program is part of the *samba*(7) suite.

**winbindd** is a daemon that provides a number of services to the Name Service Switch capability found in most modern C libraries, to arbitrary applications via PAM and **ntlm_auth** and to Samba itself.

Even if winbind is not used for nsswitch, it still provides a service to **smbd**, **ntlm_auth** and the **pam_winbind.so** PAM module, by managing connections to domain controllers. In this configuration the *idmap uid* and *idmap gid* parameters are not required. (This is known as ‘netlogon proxy only mode’.)

The Name Service Switch allows user and system information to be obtained from different databases services such as NIS or DNS. The exact behaviour can be configured throught the */etc/nsswitch.conf* file. Users and groups are allocated as they are resolved to a range of user and group ids specified by the administrator of the Samba system.

The service provided by **winbindd** is called ‘winbind’ and can be used to resolve user and group information from a Windows NT server. The service can also provide authentication services via an associated PAM module.

The pam_winbind module supports the *auth*, *account* and *password* module-types. It should be noted that the *account* module simply performs a *getpwnam*() to verify that the system can obtain a uid for the user, as the domain controller has already performed access control. If the *libnss_winbind* library has been correctly installed, or an alternate source of names configured, this should always succeed.

The following nsswitch databases are implemented by the winbindd service:

+   - **hosts**  This feature is only available on IRIX. User information traditionally stored in the *hosts*(5) file and used by **gethostbyname**(3) functions. Names are resolved through the WINS server or by broadcast.

+   - **passwd**  User information traditionally stored in the *passwd*(5) file and used by **getpwent**(3) functions.