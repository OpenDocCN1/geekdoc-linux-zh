
user::rw-
group::r--
mask::r--
other::---

Linux also allows you to set a default ACL on a directory that is automatically inherited by any file created in the directory. This feature is called *inheritance*.
To create a default ACL on a directory, start the rule with a *d:* followed by the normal rule definition. That looks like this:
$ sudo setfacl -m d::sales:rw /shared/sales
This example assigns the read and write permissions to the *sales* group for the /shared/sales directory. Now all files created in that folder will automatically be assigned read and write permissions for the sales group.

## Context-Based Permissions

Both the original permissions method and the advanced ACL method of assigning permissions to files and directories are called *discretionary access control* (DAC) methods. The permission is set at the discretion of the file or directory owner. There’s nothing an administrator can do to prevent users from granting full permission to others on all the files in their directories.

To provide complete protection of your Linux system, it helps to utilize some type of *mandatory access control* (MAC) method. MAC methods allow the system administrator to define security based on the context of an object in the Linux system to override permissions set by file and directory owners. MAC methods provide rules for administrators to restrict access to files and directories not only to users but also to applications running on the system.

> **NOTE**
> You may also see the term *role-based access control* (RBAC) used in security literature. The RBAC method is a subcategory of MAC, basing security permissions on the roles users and processes play in the Linux system.

- There are currently two popular MAC implementations in Linux:
  - SELinux for Red Hat-based systems
  - AppArmor for the Ubuntu system

The following sections provide more detail on using SELinux and AppArmor in your Linux environment.

### Using SELinux

The *Security-Enhanced Linux (SELinux)* application is a project of the U.S. National Security Agency (NSA) and has been integrated into the Linux kernel since version 2.6.x. It is now a standard part of Red Hat-based Linux distributions, such as Fedora, Rocky, and CentOS, and an optional installation for Debian-based distributions.

SELinux implements MAC security by allowing you to set policy rules for controlling access between various types of objects on the Linux system, including users, files, directories, memory, network ports, and processes. Each time a user or process attempts to access an object on the Linux system, SELinux intercepts the attempt and evaluates it against the defined policy rules.

### Enabling SELinux

The `/etc/selinux/config` file controls the basic operation of SELinux. There are two primary settings that you need to specify:

SELINUX: This setting determines the operation of SELinux. Set it to `enforcing` to enable the policy rules on the system and to block any unauthorized access. When you set it to `permissive`, SELinux monitors policy rules and logs any policy violations but doesn't enforce them. The `disabled` setting value completely disables SELinux from monitoring actions on the system.

SELINUXTYPE: This setting determines which policy rules are enforced. The `targeted` setting is the default and only enforces network daemon policy rules. The `minimum` setting only enforces policy rules on specified processes. The `mls` setting uses multilayer security, providing advanced policies following the Bell-LaPadula model of security control, which is mandated by most U.S. government and military environments that require high security. It uses security classifications such as top secret, unclassified, and public. The `strict` setting enforces policy rules for all daemons but is not recommended for use anymore.

To change the state of SELinux, you can also use the `setenforce` utility from the command line. However, you can only use the utility to change SELinux between enforcing and permissive modes. To disable SELinux, you must make the change in the SELinux configuration file. To see the current mode of SELinux, use the `getenforce` utility:

```
$ sudo getenforce
Enforcing
$
```

For a more detailed listing of the SELinux status, use the `sestatus` utility:

```
$ sudo sestatus
SELinux status: enabled
SELinuxfs mount: /sys/fs/selinux
SELinux root directory: /etc/selinux
Loaded policy name: targeted
Current mode: enforcing
Mode from config file: enforcing
Policy MLS status: enabled
Policy deny_unknown status: allowed
Memory protection checking actual (secure)
Max kernel policy version: 33
$
```

After you've enabled SELinux, it starts enforcing access rules on the objects defined in a set of policies. The next sections explain how SELinux policies work.

## Understanding Security Context

SELinux labels each object on the system with a *security context*. The security context defines what policies SELinux applies to the object. The security context format is as follows:
*user:role:type:level*

The *user* and *role* attributes are used only in the multilayer security mode and can get quite complex. Systems running in the default targeted security mode only use the *type* attribute to set the object security type and control access based on that. The *level* attribute sets the security sensitivity level and clearance level. It is optional under the targeted security mode and is mostly used in highly secure environments.

To view the security context assigned to objects, add the -Z option to common Linux commands such as id, ls, ps, and netstat. For example, to view your user security context, use the following command:
$ id -Z
unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
$

The unconfined_u user security context means the user account is not assigned to a specific security policy; likewise, the unconfined_r for the role and the unconfined_t for the type. The level security context of s0-s0:c0.c1023 means the security and clearance levels for the object are also set.

To view the security context for a file, use this:
$ ls -Z test1.txt
unconfined_u:object_r:user_home_t:s0 test1.txt

Again, the user attribute is unconfined_u, but now the type attribute is set to user_home_t. You can use this attribute in a security policy to set the access for files in each account's $HOME directory.

To examine the security context assigned to a process, use the following command:
$ ps -aZ | grep sshd

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

## Using Policies

SELinux controls access to system objects based on policies. In the targeted security mode, each policy defines what objects in a specific type security context can access objects in another type security context. This is called type enforcement.

For example, an application labeled with the type security context sshd_t is only allowed to access files labeled with the type security context rpm_t. This restricts access from the application to only certain files on the system.

SELinux maintains policies as text files in the /etc/selinux directory structure. For example, all policies for the targeted security mode are under the /etc/selinux/targeted directory.

Creating your own policies can be somewhat complicated. Fortunately, SELinux includes policy groups, called modules, that you can install as standard RPM packages. Use the semodule utility to list, install, and remove policy modules in your system.
