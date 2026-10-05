# 762 CHAPTER 21 NIS AND LDAP

```
$ cat backend.module.ldif
dn: cn=module,cn=config
objectClass: olcModuleList
cn: module
lcModulepath:/usr/lib/ldap
lcModuleload: back_hdb
```

```
dn: ocDatabase=hdb,cn=config
objectClass: olcDatabaseConfig
objectClass: olcHdbConfig
lcDatabase: [=hdb]
lolcSuffix: dc=sobell,dc=com
lcDirectory: /var/lib/ldap
lolcRootDN: cn=admin, dc=sobell,dc=com
lolcRootPW: porcine
lolcConfig: set_cachesize 2097152 0
lolcConfig: set_lkm_max_objects 1500
lolcConfig: set_lkm_max_locks 1500
lolcIndex: objectClass eq
lcLastMod: TRUE
lcaccess: to attrss=userPassword by dn="cn=admin,dc=sobell,dc=com"
lolcaccess: to attrss=shadowLastChange by self write by * =
lolcaccess: to dn.base="*" by read =
lolcaccess: to * by dn="cn=admin,dc=sobell,dc=com" write by *
```

Give the following command to load this file:

```
$ sudo ldapadd -Y EXTERNAL -H ldap:/// -f backend.setup.ldif
SASL/EXTERNAL authentication started
SASL username: gidnumber=0+uidnumber=0,cn=peercreed,cn=external,cn=auth
SASL SES: 0
adding new entry "cn=module,cn=config"
adding new entry "olcDatabase=hdb,cn=config"
```

# SET UP THE FRONT END

The following sets up the DSE (the top-level entry in the LDAP directory; page 758) for the example database. Substitute the domain name you want to use for dc=sobell,dc=com.

```
$ cat t1.ldif
dn: dc=sobell,dc=com
changetype: add
objectClass: top
objectClass: dcObject
objectclass: organization
o: Sobell Associates
dc: Sobell
description: Sobell Example
```