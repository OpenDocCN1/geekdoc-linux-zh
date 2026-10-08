# 13.6. OpenLDAP Setup Overview

This section provides a quick overview for installing and configuring an OpenLDAP directory. For more details, refer to the following URLs:

+   - http://www.openldap.org/doc/admin/quickstart.html — The Quick-Start Guide on the OpenLDAP website.
- http://www.redhat.com/mirrors/LDP/HOWTO/LDAP-HOWTO.html — The Linux HOWTO from the Linux Documentation Project, mirrored on Red Hat's website.

The basic steps for creating an LDAP server are as follows:

+   1. Install the `openldap`, `openldap-servers`, and `openldap-clients` RPMs.
2. Edit the `/etc/openldap/slapd.conf` file to refer to your LDAP domain and server. Refer to Section 13.6.1 *Editing /etc/openldap/slapd.conf* for more information on how to edit this file.
3. Start `slapd` with the command:
   `/sbin/service/slapd start`
   After you have configured LDAP correctly, use `chkconfig`, `ntsysv`, and the **Services Configuration Tool** to configure LDAP at boot time. For more information about configuring services, refer to the chapter titled *Controlling Access to Services in the Red Hat Linux Customization Guide*.
4. Add entries to your LDAP directory with `ldapadd`.
5. Use `ldapsearch` to see if `slapd` is accessing the information correctly.
6. At this point, your LDAP directory should be functioning properly and you can configure any LDAP-enabled applications to use the LDAP directory.

# 13.6.1. Editing /etc/openldap/slapd.conf

In order to use the `slapd` server, you will need to modify your configuration file, `/etc/openldap/slapd.conf`. You must edit this file to specify the correct domain and server.

The `suffix` line names the domain for which the LDAP server will provide information and should be changed from:

```
suffix      "dc=your-domain, dc=com"
```

so that it reflects a fully qualified domain name. For example:

```
suffix      "dc=example, dc=com"
```

The `rootdn` entry is the Distinguished Name (DN) for a user who is unrestricted by access controls or administrative limit parameters set for operations on the LDAP directory. The `rootdn` user can be thought of as the root for the LDAP directory. In the configuration file, change the `rootdn` line from its default value to something like the example below:

```
rootdn      "cn=root, dc=example, dc=com"
```

If you intend to populate the LDAP directory over the network, change the `rootpw` line — replacing the default value with an encrypted password string. To create an encrypted password string, type the following command:

```
slappasswd
```