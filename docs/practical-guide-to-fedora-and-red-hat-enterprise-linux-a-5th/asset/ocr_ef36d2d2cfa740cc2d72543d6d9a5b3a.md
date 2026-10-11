```
$ cat sal.ldif
dn: dc=sobell,dc=com
changetype: add
dc: sobell
objectClass: dcObject
objectClass: organization
organizationName: Sobell Associates Inc.
```

The first line of sal.ldif specifies the root DN for the entry you are adding. The changetype instruction tells ldapmodify to add the entry to the directory. You can omit this instruction if you use the -a option on the ldapmodify command line or if you use the ldapadd utility in place of ldapmodify. The line that starts with dc specifies the DC (domain component). The objectClass lines specify the object classes this entry belongs to. The organizationName specifies the name of the organization this entry is part of.

The following command modifies the LDAP directory based on the sal.ldif file. The ldif filename extension is commonly used but is not required for files holding LDIF entries.

```
$ ldapmodify -xD "cn=ldapadmin,dc=sobell,dc=com" -w porcupine -f sal.ldif
adding new entry "dc=sobell,dc=com"
```

The -x option causes the server to use simple authentication. The argument following -D specifies the DN of the LDAP administrator of the directory the command is to work with (specified in step 2 on page 715). By specifying this user, this argument also specifies the DSE of the LDAP directory. (The DN of the parent of the LDAP administrator's entry specifies the DSE.) The argument following -w is the password for the LDAP administrator. For better security, you can use -W to cause ldapmodify to prompt for this password. The name of the input file follows the -f option. The ldapmodify utility reports the DN of the new entry.

The slapcat utility, which must be run as the root user of the system (not the administrator of the LDAP directory), displays all entries in the LDAP directory in LDIF format. After the executing the preceding command, there is one entry:

```
$ su -c /usr/sbin/slapcat
Password:
dn: dc=sobell,dc=com
dc: sobell
objectClass: dcObject
objectClass: organization
o: Sobell Associates Inc.
structuralObjectClass: organization
entryUUID: 13485538-7884-102e-9401-05a9df3f842a
creatorsName: cn=ldapadmin,dc=sobell,dc=com
createTimestamp: 20091208202905Z
entryCSN: 20091208202905.821337Z#000000#000#000000
modifiersName: cn=ldapadmin,dc=sobell,dc=com
modifyTimestamp: 20091208202905Z
```