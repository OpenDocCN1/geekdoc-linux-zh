# Winbind and PAM on Novell Linux Desktop

The Novell Linux Desktop (NLD) does not use a pam_stack module to get settings from a central file. This means that for each application that needs to use winbind authentication, you must add the module to the configuration file in /etc/pam.d.

We take the configuration file for sshd as an example. After incorporating the pam_winbind.so module, the file looks like Example 9-13.

Example 9-13 Configuration file /etc/pam.d/sshd after incorporating winbind

```
#PAM-1.0
auth       sufficient    pam_winbind.so
auth       required      pam_unix2.so use_first_pass # set _secrepc
auth       required      pam_nologin.so
auth       required      pam_env.so
account    required      pam_unix2.so
account    sufficient    pam_winbind.so
account    required      pam_nologin.so
password   required      pam_pwcheck.so
password   required      pam_unix2.so_first_pass use_authtok
session    required      pam_unix2.zonone # trace or debug
session    required      pam_limits.so
```

For every PAM-enabled application that you want to enable for domain users, you must add both the auth and account line for pam_winbind.so (before the nlogin lines). Also, to prevent a double password prompt, you should add the parameter use_first_pass to any pam module needing a password in the configuration file apart from the pam_winbind.so module.

# 9.4.2 How to authenticate users using LDAP and PAM

To be able to use PAM together with LDAP to authenticate users, we need to do extra configuration for LDAP.

Because the objects in the SFU-defined Active Directory schema have not the same name as the objects needed by PAM, we need some mapping entries. An example is shown in Example 9-14.

Example 9-14 Mapping entries for /etc/nss.conf file

```
pam_login_attribute sAMAccountName
pam_filter objectclass=user
pam_member_attribute msSFU0PosixMember
pam_groupdn cn=unixusergroup,dc=AD6380,dc=LOCAL
pam_password ad
```