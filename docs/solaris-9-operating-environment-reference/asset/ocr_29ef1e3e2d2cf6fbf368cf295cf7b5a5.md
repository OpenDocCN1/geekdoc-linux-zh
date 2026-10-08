# profiles 1125

# profiles — Print Execution Profiles for a User

# Synopsis

```
/bin/profiles [-l] [user...]
```

# Description

Use the profiles command, new in the Solaris 8 Operating Environment, to print on standard output names of the execution profiles that have been assigned to you or to the optionally specified user or role name. Profiles are a role-based access control (RBAC) bundling mechanism to enumerate the commands and authorizations needed to perform a specific function. profile displays the attributes for each listed executable, as the effective user and group IDs with the process runs when started by a privileged interpreter. The profile shells are pfsh, pfksh, and pfexec. Profiles can contain other profiles defined in profpath.

You can combine multiple profiles to construct the appropriate access control. When profiles are assigned, the authorizations are added to the existing set. If the same command appears in multiple profiles, the first occurrence, as determined by the ordering of the profiles, is used for process-attribute settings. For convenience, you can specify a wild-card to match all commands.

When profiles are interpreted, the profile list is loaded from user_attr. Starting with Solaris 9 release, if any default profile is defined in /etc/security/policy.conf(see policy.conf(4)), the list of default profiles is added to the list loaded from user_attr(4). Matching entries in prof_attr(4) provide the commands list.

# Options

+   -1  List the commands in each profile followed by the special process attributes such as user and group IDs.

# Examples

The following example shows the output of the profiles command. With no options, the profiles command shows the profiles for the current user.

```
mpopoke profiles
Primary Administrator
Basic Solaris User
All
mpopoke@
```

The following example shows the output of the profiles command for three users. User winsor has Primary Administrator rights, user ray has System Administrator rights, and des has the default Basic Solaris User and All rights. One way to determine whether one set of rights stops the next one is to use the All right, which is always the last one in the list.

```
mpopoke profiles winsor ray des
Primary Administrator
Basic Solaris User
```