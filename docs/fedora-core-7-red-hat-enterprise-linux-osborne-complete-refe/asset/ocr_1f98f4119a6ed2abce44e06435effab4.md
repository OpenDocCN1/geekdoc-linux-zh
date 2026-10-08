definitions are included for objects such as files. The following is a default type for any file, with attributes file_type and sysadmfile:

```
type file_t, file_type, sysadmfile;
```

The root will have its own type declaration.

```
type root_t, file_type, sysadmfile;
```

Specialized directories such as the boot directory will also have their own type.

```
type boot_t, file_type, sysadmfile;
```

More specialized rules are set up for specific targets like the Amanda server. The following example is the general type definition for amanda_t objects, those objects used by the Amanda backup server, as listed in the targeted policy's src/program/amanda.te file:

```
type amanda_t, domain, privlog, auth, nscd_client_domain ;
```

A role declaration determines the roles that can access objects of a certain type. These rules begin with the keyword **role** followed by the role and the objects associated with that role. In this example, the amanda objects (amanda_t) can be accessed by a user or process with the system role (system_r).

```
role system_r types amanda_t;
```

A more specific type declaration is provided for executables, such as the following for the Amanda server (amanda_exec_t). This defines the Amanda executable as a system administration--controlled executable file.

```
type amanda_exec_t, file_type, sysadmfile, exec_type;
```

Associated configuration files often have their own rules.

```
type amanda_config_t, file_type, sysadmfile;
```

In the targeted policy a general, unconfin ed type is created that user and system roles can access, giving complete, unrestricted access to the system. More specific rules will restrict access to certain targets like the Web server.

```
type unconfined_t, domain, privuser, privhome, privrole, privowner, admin, auth_write, fs_domain, privmem;
role system_r types unconfined_t;
role user_r types unconfined_t;
role sysadm_r types unconfined_t;
```

Types are also set up for the files created in the user home directory.

```
type user_home_t, file_type, sysadmfile, home_type;
type user_home_dir_t, file_type, sysadmfile, home_dir_type;
```