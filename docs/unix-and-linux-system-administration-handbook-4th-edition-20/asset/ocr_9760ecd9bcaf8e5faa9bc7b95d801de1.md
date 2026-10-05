# The structure of LDAP data

As an example, here's a typical (but simplified) /etc/passwd line exposed as an LDAP entry:

```
uid: ghopper
cn: Grace Hopper
userPassword: [crypt]$1$pZaGa2RL$MPJD0ocafuhHY6kyk8HQFP0
loginShell: /bin/bash
uidNumber: 1202
gidNumber: 1202
homeDirectory: /home/ghhopper
```

This notation is a sample example of LDAP, the LDAP Data Interchange Format, which is used by many LDAP-related tools and server implementations. The fact that LDAP data can be easily converted back and forth plain text is part of the reason for its success.

Entries are organized into a hierarchy through the use of "distinguished names" (attribute name: dn) that form a sort of search path. For example, the dn for user above might be

```
dn: uid=ghoper,ou=People,dc=navy,dc=mil
```

As DN, the "most significant bit" goes on the right. Here, the DNS name navy.mil has been used to structure the top levels of LDAP hierarchy. It has been broken down into two domain components (dc's), "navy" and "mil", but this is only one of several common conventions.

Every entry has exactly one distinguished name. Therefore, the entry hierarchy looks like a simple branching tree with no loops. There are, however, provisions for symbolic links between entries and for referrals to other servers.

LDAP entries are typically schematized through the use of an objectClass attribute. Object classes specify the attributes that an entry can contain, some of which may be required for validity. The schema also assigns a data type to each attribute. Object classes nest and combine in the traditional object-oriented fashion. The top level of each object class is the class named top, which specifies merely that an entry must have an objectClass attribute.

Table 19.2 shows some LDAP attributes whose meanings might not be immediately apparent.

# Table 19.2 Some common attribute names found in LDAP hierarchies

| Attribute | Stands for | What it is |
|---|---|---|
| o | Organization | Often identifies a site's top-level entry |
| ou | Organizational unit | A logical subdivision, e.g., "marketing" |
| cn | Common name | The natural name to represent the entry |
| dc | Domain component | Used at sites that model their hierarchy on DNS |
| objectClass | Object class | Schema to which this entry's attributes conform |

+   a. Typically not used by sites that model the LDAP hierarchy on DNS