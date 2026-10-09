```
```
$ cat backend.setup.ldif
dn: cn=module,cn=config
objectClass: olcModuleList
cn: module
olcModulePath: /usr/lib/ldap
olcModuleLoad: back_hdb

dn: olcDatabase=hdb,cn=config
objectClass: olcDatabaseConfig
objectClass: olcHdbConfig
olcDatabase: {1}hdb
olcSuffix: dc=sobel1,dc=com
olcDbDirectory: /var/lib/ldap
olcRootDN: cn=admin,dc=sobel1,dc=com
olcRootPW: porcupine
olcDbConfig: set_cachesize 0 2097152 0
olcDbConfig: set_lk_max_objects 1500
olcDbConfig: set_lk_max_locks 1500
olcDbConfig: set_lk_max_lockers 1500
olDbIndex: objectClass eq
olcLastMod: TRUE
olcDbCheckpoint: 512 30
olcAccess: to attrs=userPassword by dn="cn=admin,dc=sobel1,dc=com" 
       write by anonymous auth by self write by * none
olcAccess: to attrs=shadowLastChange by self write by * read
olcAccess: to dn.base="" by * read
olcAccess: to * by dn="cn=admin,dc=sobel1,dc=com" write by * read
```
```

Give the following command to load this file:

```
```
$ sudo ldapadd -Y EXTERNAL -h ldapi:/// -f backend.setup.ldif
SASL/EXTERNAL authentication started
SASL username: gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth
SASL SSF: 0
adding new entry "cn=module,cn=config"

adding new entry "olcDatabase=hdb,cn=config"
```
```

# ## SET UP THE FRONT END

The following file sets up the DSE (the top-level entry in the LDAP directory; page 758) for the example database. Substitute the domain name you want to use for dc=sobel1,dc=com.

```
```
$ cat t11.ldif
dn: dc=sobel1,dc=com
changetype: add
objectClass: top
objectClass: dcObject
objectClass: organization
dc: Sobell Associates
dc: Sobell
description: Sobell Example
```
```