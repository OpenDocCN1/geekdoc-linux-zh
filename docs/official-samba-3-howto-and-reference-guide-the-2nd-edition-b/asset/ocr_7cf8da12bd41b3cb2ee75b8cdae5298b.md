```
root# cp samba.schema /etc/openldap/schema/
```

Next, include the **samba.schema** file in **slapd.conf**. The sambaSamAccount object contains two attributes that depend on other schema files. The *uid* attribute is defined in *cosine.schema* and the *displayName* attribute is defined in the *inetorgperson.schema* file. Both of these must be included before the **samba.schema** file.

```
## /etc/openldap/slapd.conf

## schema files (core.schema is required by default)
include
/etc/openldap/schema/core.schema

## needed for sambaSamAccount
include /etc/openldap/schema/cosine.schema
include /etc/openldap/schema/inetorgperson.schema
include /etc/openldap/schema/nis.schema
include /etc/openldap/schema/samba.schema
....
```

It is recommended that you maintain some indices on some of the most useful attributes, as in the following example, to speed up searches made on sambaSamAccount ObjectClasses (and possibly posixAccount and posixGroup as well):

```
# Indices to maintain
## required by OpenLDAP
index objectclass eq

index cn pres,sub,eq
index sn pres,sub,eq
## required to support pdw_getsampwnam
index uid pres,sub,eq
## required to support pdw_getsambaprid()
index displayName pres,sub,eq

## uncomment these if you are storing posixAccount and
## posixGroup entries in the directory as well
##index uidNumber eq
##index gidNumber eq
##index memberUid eq

index sambaSID eq
index sambaPrimaryGroupSID eq
index sambaDomainName eq
```