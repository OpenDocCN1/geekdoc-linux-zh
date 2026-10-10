# Using LDAP

The Lightweight Directory Access Protocol (LDAP) is similar to NIS in some ways, but it's more sophisticated and general in purpose. A directory, in the context of LDAP, is a type of database. An LDAP server can hold data in its directories on any number of things, including, of relevance to this chapter's topic, account information for Linux computers.

Although configuring a Linux system as an LDAP server is well beyond the scope of this chapter, configuring Linux as an LDAP client for authentication is much simpler. In brief, you must configure both NSS and PAM to use LDAP in addition to (or instead of) the regular local account files.

You must first install the LDAP authentication packages. Details differ from one distribution to another, but package names are likely to be pam_ldap and nss_ldap, or something similar. (Sometimes lib comes at the start of these package names.) Locate and install these packages using your distribution's package tools.

With the packages installed, you should edit the /etc/ldap.conf file. Look for the host and base options in this file, and set them appropriately for your network:

```
host 172.24.21.102
base dc=luna,dc=edu
```

The host line specifies the hostname or IP address of the LDAP server, and base specifies the base of the LDAP directory tree in which the account information resides. If you don't know these values, ask the person who maintains your LDAP server.

To configure NSS to use LDAP, you must edit /etc/nsswitch.conf, as described earlier in "Using NIS." Chances are adding ldap to the ends of the passwd, shadow, and group lines will do what you want:

```
passwd:  compat  ldap
shadow:  compat  ldap
group:   compat  ldap
```

PAM configuration is trickier, since the details vary from one distribution to another, as described earlier in "Configuring PAM." You should add a reference to pam_ldap.so to both the auth and account stacks for any service that should use LDAP:

```
auth    sufficient   pam_ldap.so   try_first_pass
account   sufficient   pam_ldap.so
```

With these changes in place, users should be able to log in using accounts that are defined on the LDAP server.

# Understanding RADIUS

RADIUS is a network authentication protocol that's designed as a single authentication tool for several types of network access. A RADIUS server frequently has network portals as clients—dial-up network servers, wireless access points (WAPs), and so on. Each of these clients needs to authenticate users of the network as a whole, and to simplify overall network