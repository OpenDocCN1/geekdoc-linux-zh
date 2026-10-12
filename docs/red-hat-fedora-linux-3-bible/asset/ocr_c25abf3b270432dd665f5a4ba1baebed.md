```
adding new entry "cn=Sheree Glass,ou=members,dc=linuxtoys,dc=net"
```

The password shown here (which will not display as you type it) is the one you added to your slapd.conf file. In the example, I used mysecret as the password. The -x says to use simple authentication (no SASL). The -D says to use the distinguished name defined earlier in the slapd.conf file (cn=manager,dc=linuxtoys,dc=net). The -W says to prompt for the password, instead of entering it on the command line. The -f indicates the file to load (in our example, toypeople.1dif).

As the ldapadd command successfully adds each entry, it lists the distinguished name (dn) associated with each one.

+   8. **Restart the server.** You can restart the server at this point by typing the following:

```
# /etc/init.d/ldap restart
```

+   9. **Search the directory.** To make sure that everything was properly inserted into the directory, you can run the following search command:

```
$ ldapsearch -x -W -D 'cn=manager,dc=linuxtoys,dc=net' -b 'dc=linuxtoys,dc=net' '(objectClass=*)'
# extended LDIF
#
# LDAPv3
# base <dc=linuxtoys,dc=net> with scope sub
# filter: (objectClass=*)
# requesting: ALL
#
#
# linuxtoys.net
dn: dc=linuxtoys,dc=net
objectClass: top
objectClass: dcObject
objectClass: organization
dc: linuxtoys
o: Linux Toys

# manager, linuxtoys.net
dn: cn=manager,dc=linuxtoys,dc=net
objectClass: organizationalRole
cn: Manager
description: LinuxToys Address Book Administrator

# members, linuxtoys.net
dn: ou=members,dc=linuxtoys,dc=net
objectClass: top
objectClass: organizationalUnit
ou: members
```