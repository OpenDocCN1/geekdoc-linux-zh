# /etc/ldap.conf

The file /etc/ldap.conf is the configuration file for the LDAP nameservice switch library, the LDAP PAM module, and the shadow package. The file belongs to the RPM package pwdutils.

```
da51:~ # rpm -qf /etc/ldap.conf
pwdutils-3.0.7.1-17.10
da51:~ #
```

The most important options of /etc/ldap.conf are:

+   - **host.** Specifies the name(s) or IP address(es) of the LDAP server(s) to connect to.

+   - **base.** Specifies the default base distinguished name (DN) to use for searches.

+   - **ldap_version.** Specifies the version of the LDAP protocol; “3” stands for LDAPv3.

+   - **bind_policy.** Specifies what happens if the LDAP server is not reachable. The possible values are:
+     - **hard.** nss_ldap will retry connecting to the software with exponential backoff. (default)
+     - **soft.** Forbids nss_ldap from retrying failed LDAP queries.

+   - **binddn.** Specifies he distinguished name with which to bind to the directory server(s). The default is to bind anonymously.

+   - **bindpw.** Specifies the cleartext credentials ith which to bind. This option is only applicable when used with binddn above.

+   - **scope.** Specifies the search scope. Possible values are:
+     - **sub.** subtree
+     - **one.** one level
+     - **base.** base object