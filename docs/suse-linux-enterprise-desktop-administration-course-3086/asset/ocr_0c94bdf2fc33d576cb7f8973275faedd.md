This means that automount information is searched for in the following sequence: files (/etc/auto.*) are checked for the autofs configuration first, NIS is checked next, and then LDAP is checked. To avoid possible confusion, you should remove any /etc/auto.* files, because they might conflict with the configuration stored in the LDAP directory.

The automounter queries the LDAP directory for automount information. The needed schema files are already included in the OpenLDAP server package used on SUSE Linux Enterprise Server 10. The automount information is included in the /etc/openldap/schema/rfc2307bis.schema file on SUSE Linux Enterprise Server 10.

The information that is otherwise available in the /etc/auto.* files now has to exist within the LDAP directory. In the following sample LDIF file, a Services organizational unit is created that holds the information needed by the automounter:

```
# Organizational Unit "Services"
dn: ou=Services,dc=digitalairlines,dc=com
objectclass: top
objectclass: organizationalUnit
ou: Services
```

Then the entries for auto.master and auto.home can be created using the following LDIF files:

```
# auto.master
dn: nisMapName=auto.master,ou=Services,dc=digitalairlines,dc=com
objectClass: top
objectClass: nisMap
nismapname: auto.master

dn: cn=/home,nisMapName=auto.master,ou=Services,
dc=digitalairlines,dc=com
nismapname: auto.master
objectclass: top
objectclass: nisObject
nismapentry: ldap:10.0.0.254:nismapname=auto.home,ou=Services,
dc=digitalairlines,dc=com
cn: /home

# auto.home
dn: nisMapName=auto.home,ou=Services,dc=digitalairlines,dc=com
objectclass: top
objectclass: nisMap
nismapname: auto.home

dn: cn=/,nisMapName=auto.home,ou=Services,
dc=digitalairlines,dc=com
objectclass: nisObject
cn: /
nismapentry: 10.0.0.254:/home/&
nismapname: auto.home
```