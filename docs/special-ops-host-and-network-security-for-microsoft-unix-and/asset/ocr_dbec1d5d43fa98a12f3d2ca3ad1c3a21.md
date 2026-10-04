# Chapter 6 Securing Active Directory

mode is more strict in providing information to the nonprivileged users, whereas in contrast the built-in group Everyone has more rights in the mixed mode.

It is still possible to do brute-forcing usernames and other entries in Active Directory even when all precautions are observed. This is a flaw not in Directory itself, but in LDAP usage of access rights. The point is, although we may not be authorized to view an entry in the directory, we are always informed of its existence. Compare the following two outputs (both made using an anonymous connection).

In this example, we are to see if the user Administrator exists:

```
***Searching...
ldap_search_s(1d, "CN=Administrator;CN=Users;DC=witt;DC=home", 2,
(objectclass=*", attrList, 1, &msg)
Result <0>; (null)
Matched DNs:
Getting 0 entries:
```

Note that there is no data returned, but the result is null, which means a positive match. And for a non-existing user:

```
***Searching...
ldap_search_s(1d, "CN=nonexistentuser;CN=Users;DC=witt;DC=home", 2,
(objectclass=*", attrList, 1, &msg)
Error: Search: No Such Object. <32>
Result <32>: 0000208D: NameErr: DSID-031001C9, problem 2001 (NO_OBJECT),\ondata 0, best match of: 'CN-Users,DC=witt,DC=home'
```

You can see that there is no such object in the directory, because the query returned an error in result.

# Active Attacks

This section features a selection of attacks on Active Directory and related services. These attacks are more intrusive than those we conducted on the reconnaissance stage and have the goal of obtaining access to the network services using Active Directory or simply disabling some of these services (denial of service [DoS] attacks). Most of the network-based attacks, as was noted in the previous