dlogin account sufficient       /usr/lib/security/pam_winbind.so
dlogin account requisite /usr/lib/security/$ISA/pam_roles.so.1
dlogin account required /usr/lib/security/$ISA/pam_unix.so.1
# other account sufficient      /usr/lib/security/pam_winbind.so
other account requisite /usr/lib/security/$ISA/pam_roles.so.1
other account required /usr/lib/security/$ISA/pam_unix.so.1
# Session management
#
other session required /usr/lib/security/$ISA/pam_unix.so.1
# Password management
#
*other     password sufficient        /usr/lib/security/pam_winbind.so
other password required /usr/lib/security/$ISA/pam_unix.so.1
dtssession auth required /usr/lib/security/$ISA/pam_unix.so.1
#
# Support for Kerberos V5 authentication (uncomment to use Kerberos)
#
#rdlogin auth optional /usr/lib/security/$ISA/pam_krb5.so.1 try_first_pass
#login auth optional /usr/lib/security/$ISA/pam_krb5.so.1 try_first_pass
#rdlogin auth optional /usr/lib/security/$ISA/pam_krb5.so.1 try_first_pass
#other auth optional /usr/lib/security/$ISA/pam_krb5.so.1 try_first_pass
#rdlogin account optional /usr/lib/security/$ISA/pam_krb5.so.1
#other account optional /usr/lib/security/$ISA/pam_krb5.so.1
#rdother session optional /usr/lib/security/$ISA/pam_krb5.so.1
#other password optional /usr/lib/security/$ISA/pam_krb5.so.1 try_first_pass

I also added a *try_first_pass* line after the *winbind.so* line to get rid of annoying double prompts for passwords.

Now restart your Samba and try connecting through your application that you configured in the *pam.conf*.

# 23.6  Conclusion

The Winbind system, through the use of the NSS, PAMs, and appropriate Microsoft RPC calls, have allowed us to provide seamless integration of Microsoft Windows NT domain users on a UNIX system. The result is a great reduction in the administrative cost of running a mixed UNIX and NT network.