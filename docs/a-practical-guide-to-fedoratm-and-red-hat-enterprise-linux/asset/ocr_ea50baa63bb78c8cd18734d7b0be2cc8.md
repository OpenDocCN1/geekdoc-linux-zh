The DN shows that the new employee is at the third level of the directory structure: The first level is `dc=brillserve,dc=com`; `ou=employees,dc=brillserve,dc=com` is at the second level; and `cn=Zach Brill,ou=employees,dc=brillserve,dc=com`, the employee, is at the third level.

The following example adds another employee at the third level:

```
$ cat DD.1dif
dn: cn=Sam the Great,ou=employees,dc=brillserve,dc=com
changetype: add
cn: Sam the Great
objectClass: inetOrgPerson
mail: sam@brillserve.com
givenName: Sam
surname: the Great
displayName: Sam the Great
telephoneNumber: 888 888 8888
homePhone: 111 111 1111
initials: SLS
```

```
$ ldapmodify -xD "cn=ldapadmin,dc=brillserve,dc=com" -w porcupine -f DD.1dif
adding new entry "cn=Sam the Great,ou=employees,dc=brillserve,dc=com"
```

The next example uses the `ldapmodify` modify instruction to replace the `mail` attribute value and add a title attribute for the employee named Sam the Great. The hyphen on a line by itself separates multiple modifications in a single file. Because the file specifies Sam’s DN, the server knows which entry to modify.

```
$ cat EE.1dif
dn: cn=Sam the Great,ou=employees,dc=brillserve,dc=com
changetype: modify
replace: mail
mail: sls@brillserve.com
-
add: title
title: CTO
```

```
$ ldapmodify -xD "cn=ldapadmin,dc=brillserve,dc=com" -w porcupine -f EE.1dif
modifying entry "cn=Sam the Great,ou=employees,dc=brillserve,dc=com"
```

You can use `ldapsearch` to verify the change. The final example deletes Sam from the LDAP directory:

```
$ cat FF.1dif
dn: cn=Sam the Great,ou=employees,dc=brillserve,dc=com
changetype: delete
```

```
$ ldapmodify -xD "cn=ldapadmin,dc=brillserve,dc=com" -w porcupine -f FF.1dif
deleting entry "cn=Sam the Great,ou=employees,dc=brillserve,dc=com"
```