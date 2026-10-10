```
system_u:system_r:sshd_t:s0-s0:c0.c1023 ? Ss 0:00
/usr/sbin/sshd [...]
$
```

The process required for the sshd application is set to the system_u user security context and system_r role security context. These indicate that the process is system related. The type security context for the process is different, which means it can be controlled with separate policies.

> **NOTE**
> You'll often see the security context referred to as a label in SELinux documentation and literature. SELinux must assign the label to each object on the system when it's first enabled, which can be a long process.

The semanage utility allows you to view and set the security context for user accounts on the system. For files and directories, the Linux system sets their security context when they are created, based on the security context of the parent directory. You can change the default security context assigned to a file by using the chcon or the restorecon utility.

The chcon format is as follows:

```
chcon -u newuser -r newrole -t newtype filename
```

The newuser, newrole, and newtype values define the new user, role, and type security contexts you want assigned to the specified file.

The restorecon utility restores the security context of a file or directory back to the default settings as defined in the policies. You can use the -R option to recursively restore the security context on all files under a specified directory.

> **WARNING**
> The runcon utility allows you to start an application with a specified security context, but be careful. If an application starts without having access to any required configuration or logging files, strange things can, and usually will, happen.

# Using Policies

SELinux controls access to system objects based on policies. In the targeted security mode, each policy defines what objects in a specific type security context can access objects in another type security context. This is called type enforcement.

For example, an application labeled with the type security context sshd_t is only allowed to access files labeled with the type security context rpm_t. This restricts access from the application to only certain files on the system.

SELinux maintains policies as text files in the /etc/selinux directory structure. For example, all policies for the targeted security mode are under the /etc/selinux/targeted directory.

Creating your own policies can be somewhat complicated. Fortunately, SELinux includes policy groups, called modules, that you can install as standard RPM packages. Use the semodule utility to list, install, and remove policy modules in your system.