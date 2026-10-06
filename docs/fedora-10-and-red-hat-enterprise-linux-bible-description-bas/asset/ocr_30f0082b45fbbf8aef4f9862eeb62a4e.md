# Part IV: Fedora RHEL Network and Server Setup

Other schemas you might use rely often on these schemas being included. So, unless you know don't need them, don't delete any of these schemas:

```
include /etc/openldap/schema/corba.schema
include /etc/openldap/schema/core.schema
include /etc/openldap/schema/cosine.schema
include /etc/openldap/schema/duaconf.schema
include /etc/openldap/schema/dyngroup.schema
include /etc/openldap/schema/inetorgperson.schema
include /etc/openldap/schema/java.schema
include /etc/openldap/schema/misc.schema
include /etc/openldap/schema/nis.schema
include /etc/openldap/schema/openldap.schema
include /etc/openldap/schema/ppolicy.schema
include /etc/openldap/schema/collective.schema
```

Because schemas are plain text, you can open them with any text editor to read what they do. Several of the schemas are of interest to you. The core.schema is required for all LDAP directories. The cosine and inetorgperson.schema files are particularly useful (and needed for this procedure). The nis.schema file is used to Provide Network Information System in an LDAP directory. The misc.schema file contains miscellaneous mail-related schema definitions.

> TIP: The LDAP Schema Viewer (http://ldap.akkhome.com) enables you to view object classes, attributes, syntaxes, and matching rules for common schemas for LDAP. Definitions also point to RFCs that fully define each object class.

+   3. Add backend database definitions. In the slapd.conf file, you need to define some backend database definitions. Each set of backend definitions applies to a group of databases of the same type.

Here's an example of how the backend database definitions would appear for a computer in the domain named linuxuxoys.net (of course, you would replace linuxuxoys and net with those of your domain):

```
######################################
# ldbm and/or bdb database definitions
######################################

database     bdb
suffix       "dc=linuxuxoys,dc=net"
directory    /var/lib/ldap
rootdn       "cn=Manager,dc=linuxuxoys,dc=net"
cachesize   10000
searchstack 8
dbnosync
dirty-read
```