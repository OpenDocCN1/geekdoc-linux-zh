user accordingly. To do this, you add the user to the **local. users** file in the policy users directory, as in * /etc/selinux/targeted/policy/users/local. users*. Note that this is different from the **local. users** file in the src directory, which is compiled directly into the policy. The user rules have the syntax

```
user username roles { ro lelist };
```

The following example adds the **sysadm** role to the **george** user:

```
user george roles { user_r sysadm_r };
```

Once the role is added, you have to reload the policy.

```
make reload
```

You can also manage users with the **seuser** command. To see what users are currently active, you can list them with the **seuser** command and the **show users** option.

```
# seuser show users
system_u: system_r
user_u: user_r sysadm_r system_r
root: user_r sysadm_r system_r
```

The **seuser** command has **add**, **delete**, **change**, and **rename** options for managing users. The **add** and **change** options let you specify roles to add to a user, whereas the **delete** option will remove the user.

# Runtime Security Contexts and Types: Contexts

Several applications and services are security aware and will need default security configuration information such as security contexts. Runtime configurations for default security contexts and types are kept in files located in the policy context directory, such as * /etc/selinux/targeted/contexts*. Types files will have the suffix *_types*, and security context files will use *_context*. For example, the default security context for removable files is located in the **removable_context** file. The contents of that file are shown here:

```
system_u:object_r:removable_t
```

The **default_context** file is used to assign a default security context for applications. In the strict policy it is used to control system admin access, providing it where needed, for instance, during the login process.

The following example sets the default roles for users in the login process:

```
system_r: local_login_t user_r: user_t
```

This would allows users to log in either as administrators or as regular users.

```
system_r:local_login_t sysadm_r: sysadm_t user_r: user_t
```

This next example is for remote user logins, where system administration is not included:

```
system_r:remote_login_t user_r: user_t staff_r: staff_t
```