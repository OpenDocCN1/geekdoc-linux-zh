Therefore, any user that has been granted the Media Backup profile can execute the previous backup commands with an effective userID of 0 (superuser).

In the prof_attr database, we also saw that the Operator profile consisted of a profile named All. Again, All did not have authorizations associated with it. When we look at the exec_attr database for a definition of the All profile, we get this entry:

```
All:suser:cmd:::*:
```

Examining each field, we see that All is the profile name, the security policy is suser, and the type of entity is cmd. The attribute field has an *.

It’s common to grant all users the All profile. The * is a wildcard entry that matches every command. In other words, the user has access to any command while working in the shell. Without the All profile, a user would have access to the privileged commands, but no access to normal commands such as ls and cd. Notice that no special process attributes are associated with the wildcard, so the effect is that all commands matching the wildcard run with the UID and GID of the current user (or role). Always assign the All profile last in the list of profiles. If it is listed first, no other rights are consulted when you look up command attributes.

# CHAPTER SUMMARY

This chapter has taken a look at Role-Based Access Control for delegating limited administrative capabilities to non-root users. It described the features that are inherent with RBAC, which include the following:

+   - Roles. Special user accounts intended for performing a set of administrative tasks.
- Authorizations. Sometimes referred to as “rights” that grant access to an otherwise restricted function.
- Execution profiles. Bundling mechanisms for grouping authorizations and commands with special attributes. Execution profiles are similar to the concept of setting the UID and GID permission bits on executable files.

# KEY TERMS

+   - RBAC
- Role account
- Authorization
- RBAC databases (know the specifics of all four)
- Rights profile