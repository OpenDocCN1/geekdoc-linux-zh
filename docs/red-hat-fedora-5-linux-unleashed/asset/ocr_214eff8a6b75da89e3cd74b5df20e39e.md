```
dn: cn=Paul Hudson,ou=People,dc=Hudzilla,dc=org
objectClass: inetOrgPerson
cn: Paul Hudson
cn: Hudzilla
mail: paul@Hudzilla.org
jpegPhoto: < file:///home/paul/paulHudson.jpg
sn: Hudson
```

```
dn: cn=Andrew Hudson,ou=People,dc=Hudzilla,dc=org
objectClass: inetOrgPerson
cn: Andrew Hudson
cn: IzAndy
mail: andrew@Hudzilla.org
sn: Hudson
```

```
dn: cn=Nick Veitch,ou=People,dc=Hudzilla,dc=org
objectClass: inetOrgPerson
cn: Nick Veitch
cn: CracKAttackKing
mail: nick@Hudzilla.org
sn: Veitch
```

There are three entries there, again separated by empty lines. Each person has a DN that is made up of his common name (CN), organizational unit (OU), and domain components (DCs). He also has an `objectClass` definition, `inetOrgPerson`, which gives him standard attributes like an email address, a `photograph`, and a telephone number. Entities of type `inetOrgPerson` must have a CN and an SN (surname), so you will see them in this code.

Note also that each person has two common names: his actual name and a nickname. Not all LDAP clients support more than one CN, but there is no harm in having several as long as the main one comes first and is listed in the DN.

> **TIP**
> 
> Having multiple key/value pairs, like multiple CNs, is one of the defining features of LDAP. In today’s interconnected world, few people can be defined using a single set of attributes because they have home phone numbers, work phone numbers, cell phone numbers, pager numbers, plus several email addresses, and potentially even a selection of offices where they hot desk. Using multiple CNs and other attributes allows you to properly record these complex scenarios.

The `jpegPhoto` attribute for the first entity has very particular syntax. Immediately after the colon you use an opening angle bracket (<) followed by a space and then the location of the person’s picture. Because the picture is local, it is prefixed with `file://`. It is in `/home/paul/paulHudson.jpg`, so the whole URL is `file:///home/paul/paulHudson.jpg`.