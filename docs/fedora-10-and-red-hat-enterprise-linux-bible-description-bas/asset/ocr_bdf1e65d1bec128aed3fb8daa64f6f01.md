# Part IV: Fedora and RHEL Network and Server Setup

```
add cn:
  Shree Glass
add mail:
  shree@linxtoys.net
add givenname:
  Shree
add sn:
  Glass
```

The password shown here (which will not display as you type it) is the one added to the slapd.conf file. In the example, I used mysecret as the password. The -x says to use simple authentication (no SASL). The -D says to use the distinguished name defined in the slapd.conf file (cn=Manager, dc=linxtoys, dc=net). The -f says to prompt for the password, instead of entering it in the command line.

As the ldapadd command successfully adds each entry, it lists the objects associated with each one.

+   8. Restart the server. You can restart the server at this point by typing the following:
# /etc/init.d/ldap restart

+   9. Search the directory. To make sure everything was properly inserted into the directory, you can run the following search command:

```
# ldapsearch -x -W -D 'cn=manager, dc=linxtoys, dc=net' \
-B 'dc=linxtoys, dc=net' '(objectClass=*)'
# extended LDIF
#n# LDAPv3
# base <dc=linxtoys, dc=net> with scope subtree
# filter: (objectClass=*)
# requesting: ALL

# linxtoys.net
dn: dc=linxtoys, dc=net
objectClass: top
objectClass: dcObject
objectClass: organization
dc: linxtoys
o: Linux Toys
```