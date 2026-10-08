# Files

```
```
/usr/share/lib/tmac/tmac.bib
File of macros used by nroff/troff.
```
```

# Attributes

See attributes(5) for descriptions of the following audited attributes:

| Attribute Type | Attribute Value |
|---|---|n| Availability | SUNdoc |

# See Also

addbib(1), indxbib(1), lookbib(1), nroff(1), refer(1), sortbib(1)
troff(1), attributes(5)

# Bugs

Users must rewrite macros to create customized formats.

# New roles — Print Roles Granted to a User

# Synopsis

```
```
bin/roles [user...]
```
```

# Description

The roles command, new in the Solaris 8 Operating Environment, to print on standard output the role-based access control (RBAC) roles that you or the optionally specified user have been granted. Roles are special accounts that correspond to a functional responsibility instead of an actual person (referred to as a normal user).
Each user can have zero or more roles. Roles have most of the attributes of normal users and are identified like normal users in passwd(4) and shadow(4). Each role must have an entry in the user_attr(4) file that identifies it as a role. Roles can have their own authorizations and profiles. See auths(1) and profile(1).
Roles cannot log in to a system as a primary user. A user must first log in as himself and then assume the role. The actions of role are attributable to the normal user. When auditing is enabled, the audited events of the role contain the ID of the original user who assumed the role.
A role counts itself and any assigned roles. Roles are not hierarchical. However, starting with the Solaris 9 release profiles (see prof_attr(4)) are hierarchical, and you can use them to achieve the same effect as hierarchical roles.
Roles must have valid passwords and one of the shells that interprets profiles—either pfscsh, pksh, or pfsh. See pfexec(1).
Users can assume roles with su(1M), login(1), or some other service that supports the PAM_USER variable. To successfully assume a role, the user must be a member of the role and know the role password. Role assignments are specified in user_attr(4).