# # File Contexts

File contexts associate specific files with security contexts. The file or files are listed first, with multiple files represented with regular expressions. Then the role, type, and security level are specified. The following creates a security context for all files in the /etc directory (configuration files). These are accessible from the system user (system_u) and are objects of the etc_t type with a security level of 0, s0.

```
/etc(/.*)?                  system_u:object_r:etc_t:s0
```

Certain files can belong to other types; for instance, the **resolve.conf** configuration file belongs to the net_conf type.

```
/etc/resolve\\.conf\.*    --    system_u:object_r:net_conf_t:s0
```

Certain services will have their own security contexts for their configuration files.

```
/etc/amanda(/.*)?              system_u:object_r:amanda_config_t:s0
```

File contexts are located in the **file_contexts** file in the policy’s contexts directory, such as /etc/selinux/targeted/contexts/files/file_contexts. The version used to create or modify the policy is located in the policy modules active directory, as in **targeted/modules/active/file_contexts**.

# # User Roles

User roles define what roles a user can take on. Such a role begins with the keyword **user** followed by the user name, then the keyword **roles**, and finally the roles it can use. You will find these rules in the selinux reference policy source code files. The following example is a definition of the system_u user:

```
user system_u roles system_r;
```

If a user can have several roles, then they are listed in brackets. The following is the definition of the standard user role in the targeted policy, which allows users to take on system administrative roles:

```
user user_u roles { user_r sysadm_r system_r };
```

The strict policy lists only the user_r role.

```
user user_u roles { user_r };
```

# # Access Vector Rules: allow

Access vector rules are used to define permissions for objects and processes. The **allow** keyword is followed by the object or process type, and then the types it can access or be accessed by and the permissions used. The following allows processes in the amanda_t domain to search the Amand a configuration directories (any directories of type amanda_config_t):

```
allow amanda_t amanda_config_t:dir search;
```