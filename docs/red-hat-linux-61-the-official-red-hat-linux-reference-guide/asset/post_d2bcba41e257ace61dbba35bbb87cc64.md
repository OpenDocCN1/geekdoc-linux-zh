
## Chapter 13. Lightweight Directory Access Protocol (LDAP) 187

### 13.3. OpenLDAP Daemons and Utilities

The suite of Open LDAP libraries and tools is spread out over the following packages:

- openldap — Contains the libraries necessary to run the OpenLDAP server and client applications.
- openldap-clients — Contains command line tools for viewing and modifying directories on an LDAP server.
- openldap-servers — Contains the servers and other utilities necessary to configure and run an LDAP server.

To perform administrative tasks, the openldap-servers package installs the following utilities into:

- slapadd — Adds entries from an LDIF file to an LDAP directory. For example, the command /usr/sbin/slapadd -l ldif-output writes to the LDIF file, ldif-output, containing the new entries.
- slapcat — Pulls entries out of an LDAP directory in the default format — Berkeley — saves them in an LDIF file. For example, the command /usr/sbin/slapcat -l ldif-output will output an LDIF file called ldif-output containing the entries from the LDAP directory.
- slapindex — Re-indexes the slapd directory on the current content.
- slappasswd — Generates an encrypted user password value for use with ldapmodify or modify the root pw in the slapd configuration file, /etc/openldap/ldap.conf. Execute the /usr/sbin/slpasswd command to create the password.

**Warning**
Be sure to stop slapd by issuing /usr/sbin/service slapd stop before using slapadd, slapcat or slapindex. Otherwise, the integrity of the LDAP directory is at risk.

For more information about how to use these utilities, see their respective man pages.

The openldap-clients package installs tools into /usr/bin/ which are used to add, modify, and delete entries in an LDAP directory. These tools include the following:

- ldapmodify — Modifies entries in an LDAP directory, accepting input via a file or standard input; ldapadd — Adds entries to your directory by accepting input via a file or standard input; ldapadd is actually a link to ldapmodify -a.
- ldapsearch — Searches for entries in the LDAP directory using a shell prompt.
- ldapdelete — Deletes entries from an LDAP directory by accepting input via user input at the terminal or via a file.

With the exception of ldapsearch, each of these utilities is most used by referencing a file containing the changes to be made rather than typing a command for each entry you wish to change in an LDAP directory. The format of such a file is outlined in each application's man page.

## Chapter 13. Lightweight Directory Access Protocol (LDAP)

### 13.3.1. NSS, PAM, and LDAP

In addition to the OpenLDAP packages, Red Linux includes a package called nss_ldap which enhances LDAP's ability to integrate into both Linux and UNIX environments.

The nss_ldap package provides the following modules:

- /lib/libnss_ldap-<glibc-version>.so
- /lib/security/pam_ldap.so

The libnss_ldap-<glibc-version>.so module allows applications to look up users, groups, hosts, and other information in an LDAP directory via glibc's Nameservice Switch (SSS) interface. NSS allows applications to authenticate using LDAP in conjunction with the Network Information Service (NIS) name service and authentication files.

The pam_ldap module allows PAM-aware applications to authenticate users using information stored in an LDAP directory. PAM-aware applications include console login, POP and IMAP mail servers, and Samba. By deploying an LDAP server on your network, all of these applications can authenticate using the same user ID and password combination, greatly simplifying administration.

### 13.3.2. PHP4, the Apache HTTP Server, and LDAP

Red Linux includes a package containing an LDAP module for the PHP server-side scripting language.

The php-ldap package adds LDAP support to the PHP4 HTML-embedded scripting language via the /usr/lib/php4/ldap.so module. This module allows PHP4 scripts to access information stored in an LDAP directory.

![](img/31025704b51d5760c0228ff0f3db98bf_203_0.png)

> Red Linux no longer ships with the auth_ldap package. This package provided LDAP support for versions 1.3 and earlier of the Apache HTTP Server. See the Apache Software Foundation website at http://www.apache.org/ for details on the status of this module.

### 13.3.3. LDAP Client Applications

There are graphical LDAP clients available which support creating and modifying directories, but they do not ship with Red Linux. One such application is LDAP Browser/Editor — A Java-based tool available at http://www.iet.edu/~gawojar/ldap.

Other LDAP clients access directories as read-only, using them to retrieve, but not alter, organization-wide information. Some examples of such applications are Mozilla-based Web browsers, Sendmail, Balsa, Paine, Evolution, and Gnome Meeting.

### 13.4. OpenLDAP Configuration Files

OpenLDAP configuration files are installed into the /etc/openldap/ directory. The following is a brief list highlighting the most important directories and files:

- /etc/openldap/ldap.conf — This is the configuration file for all client applications which use the OpenLDAP libraries such as ldsearch, ldapd, Sendmail, Pine, Balsa, Evolution, and Gnome Meeting.
- /etc/openldap/slapd.conf — This is the configuration file for the slapd daemon. See Section 13.6 Editing /etc/openldap/slapd.conf for more information about this file.
- /etc/openldap/schema/ — This subdirectory contains the schema used by the slapd daemon. See Section 13.5 The /etc/openldap/schema/ Directory for more information about this directory.

> Note
> If the nss_ldap package is installed, it will create a file named /etc/ldap.conf. This file is used by the PAM and NSS modules supplied by the nss_ldap package. See Section 13.7 Configuring Your System to Authenticate Using OpenLDAP for more information about this configuration.

### 13.5. The /etc/openldap/schema/ Directory

The /etc/openldap/schema/ holds LDAP definitions, previously located in the slapd.at and slapd.conf files. All attribute syntax definitions and objectclass definitions are now located in the different schema files. The various schema files are referenced in /etc/openldap/schema.conf using include:

```
include core.schema
include cosine.schema
include person.schema
include nis.schema
include inetd.schema
include kerberos.schema
include member.schema
include mail.schema
include device.schema
include posix.schema
```

> **Caution**
> Extending the schema to match specialized requirements is involved and beyond the scope of this chapter. You should not modify any schema files installed by LDAP.

### 13.6. OpenLDAP Setup

This section provides a quick overview for installing and configuring LDAP. For more details, refer to the following URLs:

- http://www.ldap.org/quickstart.html — The Quick-Start Guide on LDAP.
- http://www.redhat.com/LDAP-HOWTO.html — The Documentation Project.

The basic steps for creating an LDAP server are as follows:

1. Install the `openldap`, `openldap-servers`, and `openldap-clients` RPMs.
2. Edit the `/etc/openldap/slapd.conf` file to refer to your LDAP domain and server.
3. Start `slapd` with the command: `/sbin/service slapd start`
   After you have configured LDAP correctly, use `chkconfig`, `ntsysv`, and the **Services Configuration Tool** to configure LDAP at boot time.
4. Add entries to your LDAP directory with `ldapadd`.
5. Use `ldapsearch` to see if `slapd` is accessing the information correctly.
6. At this point, your LDAP directory should be functioning properly and you can configure any LDAP-enabled applications to use the directory.

### 13.6.1. Editing /etc/openldap/slapd.conf

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
