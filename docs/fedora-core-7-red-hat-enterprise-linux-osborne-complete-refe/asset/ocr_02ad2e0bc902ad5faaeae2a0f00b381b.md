The following example allows Amanda to read the files in a user home directory:

```
allow amanda_t user_home_type:file { getattr read };
```

The next example allows Amanda to read, search, and write files in the Amanda data directories:

```
allow amanda_t amanda_data_t:dir { read search write };
```

# Role Allow Rules

Roles can also allow rules. Though they can be used for domains and objects, they are usually used to control role transitions, specifying whether a role can transition to another role. These rules are listed in the rbac configuration file. The following entry allows the user to transition to a system administrator role:

```
allow user_r sysadm_r;
```

# Transition and Vector Rule Macros

The type transition rules set the type used for rules to create objects. Transition rules also require corresponding access vector rules to enable permissions for the objects or processes. Instead of creating separate rules, macros are used that will generate the needed rules. The following example sets the transition and access rules for user files in the home directory using the file_type_auto_trans macro:

```
file_type_auto_trans(privhome, user_home_dir_t, user_home_t)
```

The next example sets the Amanda process transition and access rules for creating processes:

```
domain_auto_trans(inetd_t, amanda_inetd_exec_t, amanda_t)
```

# Constraint Rules

Restrictions can be further placed on processes such as transitions to ensure greater security. These are implemented with constraint definitions in the constraints file. Constraint rules are often applied to transition operations, such as requiring that, in a process transition, user identities remain the same, or that process 1 be in a domain that has the privuser attribute and process 2 be in a domain with the userdomain attribute. The characters u, t, and r refer to user, type, and role.

```
constrain process transition
   ( u1 == u2 or ( t1 == privuser and t2 == userdomain ) )
```

# SELinux Policy Configuration Files

Configuration files are normally changed using .te and .fc files. These are missing from the module headers in /usr/share/selinux. If you are adding a module, you will need to create the .te and .fc files for it. Then you can create a module and add it as described in the next section.