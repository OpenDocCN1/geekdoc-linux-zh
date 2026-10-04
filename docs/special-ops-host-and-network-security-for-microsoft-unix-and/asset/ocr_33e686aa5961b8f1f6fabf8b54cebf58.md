# LDAP

Lightweight Directory Access Protocol (LDAP) is a protocol that enables clients to access information within a directory service. LDAP was created after X.500, a directory service standard protocol, because of the overhead and subsequent slow response of heavy X.500 clients, hence the name lightweight. LDAP clients are able to access Active Directory, which opens Active Directory up to clients other than those that access Windows 2000 in a standard fashion.

You have noticed that even the naming scheme of Active Directory follows LDAP principles. Microsoft produced a very good tool called LDAPexe (it is included in the Windows 2000 Resource Kit), which allows a low-level browsing of Active Directory contents through the LDAP interface. Figure 6.3 is an example of some information (the most interesting items are in bold) produced during the anonymous connection to Active Directory server—a domain controller for the witt.home domain. You will see that the extent of the information given by Active Directory is much bigger and can be used for pre-attack reconnaissance.

> Note Lightweight Directory Access Protocol operates on TCP port 389 by default.

# Figure 6.3 Dump of LDAP Connection to Active Directory Server

```
ld = ldap_open("localhost", 389);
Established connection to localhost.
Retrieving base DSA information...
Result <0>: (null)
Matched DNs:
Getting 1 entries:
>> Dn:
1> currentTime: 12/18/2002 19:16:16 GMT Standard Time GMT Daylight Time:
1> subschemaEntry: CN=Aggregate,CN=Schema, CN=Configuration,DC=witt,
DC=home:
1> dsServiceName: CN=NTDS Settings,CN=TEST1,CN=Servers,CN=Default-First-
```