# config: The SELinux Configuration File

The `/etc/selinux/config` file, which has a link at `/etc/sysconfig/selinux`, controls the state of SELinux on the local system. Although you can modify this file, it might be more straightforward to work with `system-config-selinux` (next page). In the following example, the policy is set to targeted, but that setting is of no consequence because SELinux is disabled:

```
$ cat /etc/selinux/config
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=disabled
# SELINUXTYPE= can take one of these two values:
#     targeted - Targeted processes are protected.
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
```

To put SELinux in enforcing mode, change the line containing the **SELINUX** assignment to `SELINUX=enforcing`. Similarly, you can change the policy by setting `SELINUXTYPE`. The change takes effect when the system reboots.

# If you will use SELinux in the future

> If you will use SELinux in the future but not now, turn it on when you install Linux and run it in permissive state with the policy set to the policy you will eventually use. Permissive state writes the required extended information to inodes, but it does not stop you from doing anything on the system.

If you turn on SELinux after it has been disabled, when you reboot the system SELinux has to add extended attributes to the files in the filesystem. This process can take a long time on a large file-system. If you are never going to use SELinux, disable it.

# getenforce, setenforce, AND sestatus: Work with SELinux

The `getenforce` and `setenforce` utilities report on and temporarily set the SELinux state. The `sestatus` utility displays a summary of SELinux on the local system:

```
# getenforce
Enforcing

# setenforce permissive

# sestatus
SELinux status:              enabled
SELinux fs mount:            /sys/fs/selinux
SELinux root directory:      /etc/selinux
Loaded policy name:          targeted
Current mode:                permissive
```