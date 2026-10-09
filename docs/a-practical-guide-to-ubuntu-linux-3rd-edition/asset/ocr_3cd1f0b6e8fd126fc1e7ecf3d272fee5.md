```
$ ldapmodify -XD "cn=admin,dc=sobell,dc=com" -W -f sa2.1dif
Enter LDAP Password:
adding new entry "cn=Samuel Smith,ou=employees,dc=sobell,dc=com"
```

Now slapcat shows the employee you just added:

```
$ sudo slapcat
dn: dc=sobell,dc=com
---

dn: cn=Samuel Smith,ou=employees,dc=sobell,dc=com
cn: Samuel Smith
cn: smith
objectClass: inetOrgPerson
mail: s1s@example.com
givenName: Samuel
sn: Smith
displayName: Samuel L Smith
telephoneNumber: 999 999 9999
homePhone: 000 000 0000
initials: SLS
---
```

The DN shows that the new employee is at the third level of the directory structure: The first level is `dc=sobell,dc=com`; `ou=employees,dc=sobell,dc=com` is at the second level; and `cn=Samuel Smith,ou=employees,dc=sobell,dc=com`, the employee, is at the third level.

You can put as many entries in a file as you like, but each must be separated from the next by a blank line. For clarity, the examples in this section show one entry per file. The following example adds another employee at the third level:

```
$ cat sa3.1dif
dn: cn=Helen Simpson,ou=employees,dc=sobell,dc=com
changetype: add
cn: Helen Simpson
cn: simpson
objectClass: inetOrgPerson
mail: helen@sobell.com
givenName: Helen
surname: Simpson
displayName: Helen L Simpson
telephoneNumber: 888 888 8888
homePhone: 111 111 1111
initials: HLS
```

```
$ ldapmodify -XD "cn=admin,dc=sobell,dc=com" -W -f sa3.1dif
Enter LDAP Password:
adding new entry "cn=Helen Simpson,ou=employees,dc=sobell,dc=com"
```