On large installations using winbindd(8) it may be necessary to suppress the enumeration of groups through the **setgrent**, **getgrent()** and **endgrent()** group of system calls. If the `winbind enum groups` parameter is **no**, calls to the **getgrent()** system call will not return any data.

> **WARNING**
> 
> Turning off group enumeration may cause some programs to behave oddly.

# winbind enum users (G) Default: `winbind enum users = yes`

On large installations using winbindd(8) it may be necessary to suppress the enumeration of users through the **setpwent()**, **getpwent()** and **endpwent()** group of system calls. If the `winbind enum users` parameter is **no**, calls to the **getpwent** system call will not return any data.

> **WARNING**
> 
> Turning off user enumeration may cause some programs to behave oddly. For example, the finger program relies on having access to the full user list when searching for matching usernames.

# winbind nested groups (G) Default: `winbind nested groups = no`

If set to **yes**, this parameter activates the support for nested groups. Nested groups are also called local groups or aliases. They work like their counterparts in Windows: Nested groups are defined locally on any machine (they are shared between DC’s through their SAM) and can contain users and global groups from any trusted SAM. To be able to use nested groups, you need to run nss_winbind.

Please note that per 3.0.3 this is a new feature, so handle with care.

# winbind separator (G) Default: `winbind separator = \\+`

Example: `winbind separator = +`

This parameter allows an admin to define the character used when listing a username of the form of **DOMAIN\\user**. This parameter is only applicable when using the **pam_winbind.so** and **nss_winbind.so** modules for UNIX services.