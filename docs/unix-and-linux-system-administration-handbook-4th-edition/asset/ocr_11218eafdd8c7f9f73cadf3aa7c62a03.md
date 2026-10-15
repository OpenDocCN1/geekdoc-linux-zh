+   - A graphical console for all facets of user, group, and server management
+   - On-line, zero downtime, LDAP-based update of schema, configuration, management and in-tree Access Control Information (ACIs)

As of this writing, the 389 Directory Server appears to have a more active development community than OpenLDAP. We generally recommend it over OpenLDAP for new installations.

From an administrative standpoint, the structure and operation of the two open source servers are strikingly similar. This fact is perhaps not too surprising since both packages were built on the same original code base.

# LDAP instead of /etc/passwd and /etc/group

Client-side LDAP support is relatively easy to add. Some systems install the necessary nss_ldap package by default, but if not, they usually provide the package as an option. This package includes a PAM module that lets you use LDAP with pluggable authentication modules in addition to the name service switch. (See Chapter 30, Cooperating with Windows, for more information about integrating UNIX and Linux systems with Active Directory-based LDAP.)

Client-side LDAP defaults for nss_ldap are set in /etc/ldap.conf, which shares its format with /etc/openldap/ldap.conf (described on page 732) but which includes additional options specific to the name service and PAM contexts. You must also edit the /etc/nsswitch.conf file on each client to add ldap as a source for each type of data you want to LDAPify. (The nsswitch.conf changes make the C library pass requests to the libnss_ldap library, which then uses the /etc/ldap.conf information to figure out how to perform the LDAP queries. See Prioritizing sources of administrative information on page 739 for details.)

RFC2307 defines the standard mapping from traditional UNIX data sets, such as the passwd and group files, into the LDAP namespace. It's a useful reference document for sysadmins using LDAP in a UNIX environment, at least in theory. In practice, the specifications are a lot easier for computers to read than for humans; you're better off looking at examples.

Padl Software offers a free set of Perl scripts that migrate existing flat files or NIS maps to LDAP. It's available from padl.com/OSS/MigrationTools.html, and the scripts are straightforward to run. They can be used as filters to generate LDIF, or they can be run against a live server to upload the data directly. For example, the migrate_group script converts this line from /etc/group

```
csstaff:x:2033:evi,matthew,trent
```

to the following LDIF:

```
dn: cn=csstaff,ou=Group,dc=domainname,dc=com
cn: csstaff
objectClass: posixGroup
objectClass: top
```