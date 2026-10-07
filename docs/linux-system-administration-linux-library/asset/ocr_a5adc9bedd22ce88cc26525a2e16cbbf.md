# Listing 7.6 The system-auth File

```
##PAM-1.0
# This file is auto-generated.
# User changes will be destroyed the next time authconfig is run.
auth        sufficient /lib/security/pam_unix.so leaveauth nullock
                                 =md5 shadow
auth        required /lib/security/pam_deny.so
account     sufficient /lib/security/pam_unix.so
account     required /lib/security/pam_deny.so
password    required /lib/security/pam_cracklib.so retry=3
password    sufficient /lib/security/pam_unix.so nullock
                                 use_authok md5 shadow
password    required /lib/security/pam_deny.so
session     required /lib/security/pam_limits.so
session     required /lib/security/pam_unix.so
```

As a result, the next module that the auth service uses pam_unix.so, the authentication module. The parameters are likeauth, nullock, md5, and shadow. The likeauth argument makes the module return the same value when called as a credential-setting module and an authentication module. By default, it will reject a NULL password, but the nullock parameter overrides this. We prefer to remove the nullock parameter to prevent the system from accepting NULL passwords. The shadow parameter forces the system to check whether the suite ensures that the login be denied, for example if the account had expired. Passing this module is also required.

The libraries for PAM are located in /lib/security/. If you are having problems with the login process, it would be wise to check /etc/pam.d/login file to determine which PAM libraries are needed and make sure they exist in the /lib/security directory. Further, you should take some time to understand the commonly used PAM files. The better you know them, the better you'll be able to troubleshoot problems.

The beauty of PAM is in its configurability. PAM's modular design makes it easy to use and easy to change. Any application that is developed to be PAM-aware makes user's lives easier by not requiring them to learn separate passwords for each application.

To learn more about implementing PAM in Linux, see The System Administrator's Guide, at http://www.us.kernel.org/pub/linux/libs/pam/Linux-PAM-html.