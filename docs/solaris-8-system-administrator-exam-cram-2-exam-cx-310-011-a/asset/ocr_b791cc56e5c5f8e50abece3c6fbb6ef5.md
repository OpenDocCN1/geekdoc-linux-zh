# The Execution Attributes Database (exec_attr)

The /etc/security/exec_attr file is used to associate privileged operations (commands executed with a specified UID and/or GID) with profiles. You can then assign these profiles to user accounts or roles. Table 17.6 lists the colon-delimited fields of the exec_attr file.

**Table 17.6 Fields of the Execution Attributes Database**

| Field | Use |
|---|---|
| **Name** | Name of the associated profile (must match the profile name in the prof_attr file entry exactly). |
| **Policy** | Security policy. Currently, the superuser policy **suser** is the only valid entry. |
| **Type** | Type of entity. Currently, the command type **cmd** is the only valid entry. |
| **Res1** | Reserved for future use (empty field). |
| **Res2** | Reserved for future use (empty field). |
| **ID** | Command to be executed (specified using a full pathname or partial path with metacharacters). |
| **Attributes** | List of key=value pairs (separated by semicolons) that determines the attributes to apply to the command during execution. Valid keys are **euid** (set effective UID), **uid** (set real UID), **egid** (set effective GID), and **gid** (set real GID). Valid values are UIDs, user account names, GIDs, and group account names. |

The following example shows two entries from the /etc/security/exec_attr file associated with the Printer Management profile.

```
Printer Management:suser:cmd:::/usr/bin/enable:euid=lp
Printer Management:suser:cmd:::/usr/bin/disable:euid=lp
```

The first entry defines execution of the enable(1) command as a privileged operation. It will be executed with an effective UID of lp. The second entry defines execution of the disable(1) command as a privileged operation. It will also be executed with an effective UID of lp.

Table 17.7 lists the default privileged operations defined by the exec_attr file. All have the **Policy** field set to **suser** and the **Type** field set to **cmd**.