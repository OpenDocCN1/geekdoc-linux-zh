# 698 Linux Administration: A Beginner's Guide

```
dc: example

dn: cn=bogus,dc=example,dc=org
objectClass: organizationalRole
cn: bogus
```

```
dn: cn=testuser,dc=example,dc=org
objectClass: organizationalRole
cn: testuser
```

Here, we didn't need to specify explicitly the basedn to search because that information is already defined in our /etc/openldap/ldap.conf.

+   3. We'll now draw our query by searching only for the entry for the object whose common name (cn) is equals. Issue this command:

```
[root@server #] ldapsearch -x -LLL -b 'dc=example,dc=org' '(cn=bogus)'
: cn=bogus,dc=example,dc=org
objectClass: organizationalRole
cn: bogus
```

+   4. Now we'll attempt to perform a privileged operation on a directory entry using the ldapdelete utility. Let's delete the entry for the DN of cn=bogus,dc=example,dc=org. Issue this command:

```
[root@server #] ldapdelete -x -W -D \
'cn=Manager,dc=example,dc=org' \\
'cn=bogus,dc=example,dc=org'
Enter LDAP Password:
```

Enter the password for the cn=Manager,dc=example,dc=org DN to complete the operation.

+   5. We use the ldapsearch utility again to make sure that the entry has been removed. 

```
[root@server #] ldapsearch -x -LLL -b 'dc=example,dc=org' '(cn=bogus)'
```

This command should return nothing.

# Using OpenLDAP for User Authentication

Now we'll set up the OpenLDAP server (client) that we configured earlier in the chapter to manage Linux user accounts. We will be using some of the migration scripts that come with the software to pull/migrate the users that already exist in the system's /etc/passwd into LDAP.