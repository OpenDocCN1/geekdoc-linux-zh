| Table 17.8 Command-line Arguments for the roleadd Command |  |
|---|---|
| **Argument** | **Description** |
| *role* | Specifies the name of the new role (required). |
| **-A authorizations** | Specifies one or more authorizations (separated by commas). |
| **-b base** | Defines a base directory. If a home directory (**-d**) is not specified, the role name is added to *base* and used as the home directory. |
| **-c comment** | Specifies a comment placed in the comment (**gcos**) field of the `/etc/passwd` file. |
| **-d directory** | Defines the role’s home directory. |
| **-e date** | Specifies an expiration date for the role. After the specified date, the role is disabled. |
| **-f days** | Specifies the maximum number of days the role can be inactive before it is disabled. |
| **-g group** | Defines the GID or name of an existing group that will be the primary group for the role. |
| **-G group** | Defines the GID or name of an existing group that will be a secondary group for the role. |
| **-k template_dir** | Specifies the directory containing a template (default) `.profile` used for the user profile. |
| **-m** | Creates the home directory if it doesn’t exist. The home directory is defined by **-b** and the role name or **-d**. |
| **-o** | Allows an existing UID to be specified—that is, allows a role to be created with a duplicate UID (see **-u**). |
| **-p profiles** | Specifies one or more execution profiles (separated by commas). |
| **-s shell** | Specifies the login shell; the default is the Bourne shell (`/bin/sh`). |
| **-u uid** | Specifies the UID of the role. It must be a decimal integer. If not specified, the next highest available UID is assigned. |

The following example creates a role by using the **roleadd** command:

```
# roleadd -A solaris.system.date -P "Printer Management" prt_adm
#
```

This command creates the prt_adm role. It assigns the solaris.system.date authorization and the Printer Management profile to the role.

To make life a little easier, the **roleadd** command also supports the **-D** command-line argument, which allows default values to be assigned to authorizations (**-A**), base directory (**-b**), group (**-g**), expiration date (**-e**),