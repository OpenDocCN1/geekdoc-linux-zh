The first entry defines the prt_adm role that is assigned the Printer Management profile. In addition, this role is assigned the authorization solari​s.system.date, which allows the role to set the system date.

The second entry defines the prof_adm role, which is assigned all authorizations relating to RBAC profile administration. Note that the asterisk (*) metacharacter can be used to denote *any* (like the shell metacharacter).

The third entry defines the role_adm role, which is assigned all authorizations relating to RBAC role administration.

The fourth entry assigns the prt_adm role to the normal user account *amber*. Once logged in, *amber* can use the **su(1)** command to become the prt_adm and perform any tasks assigned to that role.

The fifth entry assigns the prof_adm and role_adm roles to the normal user account *Morgan*. Once logged in, *morgan* can use the **su(1)** command to become the prof_adm and role_adm, and then perform any tasks assigned to those roles.

The sixth entry assigns a considerable amount of access control to the normal user account *dana*. This control includes all authorizations associated with SolarisJobs (cron and at job management), the Printer Management profile, the prof_adm role, and the role_adm role.

The following example shows the only default entry in the user_attr file. This entry is for the root superuser account. Basically, it assigns all authorizations and profiles:

```
root::::type=normal;auths=solaris.*,solaris.grant;profiles=All
```

# The Execution Profile Attributes Database (prof_attr)

The /etc/security/prof_attr file is used to assign authorizations from the Authorization Attributes Database (auth_attr) and privileged operations from the Execution Attribute Database (exec_attr) to a single named entity referred to as an “execution profile” or just a “profile.” You can then reference these profiles in the user_attr file to assign them to roles or directly to user accounts. Table 17.2 lists the colon-delimited fields of the prof_attr file.

| Field | Use |
|---|---|
| Name | Profile name (case-sensitive). |
| Res1 | Reserved for future use (empty field). |