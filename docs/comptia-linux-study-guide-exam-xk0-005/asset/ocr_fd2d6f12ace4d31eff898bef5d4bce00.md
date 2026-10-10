# ### Using SELinux

The *Security-Enhanced Linux (SELinux)* application is a project of the U.S. National Security Agency (NSA) and has been integrated into the Linux kernel since version 2.6.x. It is now a standard part of Red Hat–based Linux distributions, such as Fedora, Rocky, and CentOS, and an optional installation for Debian-based distributions.

SELinux implements MAC security by allowing you to set policy rules for controlling access between various types of objects on the Linux system, including users, files, directories, memory, network ports, and processes. Each time a user or process attempts to access an object on the Linux system, SELinux intercepts the attempt and evaluates it against the defined policy rules.

# ### Enabling SELinux

The `/etc/selinux/config` file controls the basic operation of SELinux. There are two primary settings that you need to specify:

SELINUX: This setting determines the operation of SELinux. Set it to `enforcing` to enable the policy rules on the system and to block any unauthorized access. When you set it to `permissive`, SELinux monitors policy rules and logs any policy violations but doesn't enforce them. The `disabled` setting value completely disables SELinux from monitoring actions on the system.

SELINUXTYPE: This setting determines which policy rules are enforced. The `targeted` setting is the default and only enforces network daemon policy rules. The `minimum` setting only enforces policy rules on specified processes. The `m1s` setting uses multilayer security, providing advanced policies following the Bell-LaPadula model of security control, which is mandated by most U.S. government and military environments that require high security. It uses security classifications such as top secret, unclassified, and public. The `strict` setting enforces policy rules for all daemons but is not recommended for use anymore.

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
```