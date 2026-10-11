There is always a tradeoff between security and usability. The targeted policy is less secure than the strict policy, but it is much easier to maintain. When you run the strict policy, you will likely have to customize the policy so that users can do their work and the system can function appropriately.

You can switch from one policy to the other (as explained shortly). Despite this flexibility, it is not a good idea to switch from a targeted to a strict policy on a production system. If you do so, some users may not be able to do their work. You would need to customize the policy in such a case. Changing from a strict to a targeted policy should not create any problems.

# More Information

Web NSA: www.nsa.gov/research/selinux
Fedora SELinux wiki: fedoraproject.org/wiki/SELinux
SELinux News: selinuxnews.org
SELinux for distributions (Sourceforge): selinux.sourceforge.net
Fedora SELinux mailing list: www.redhat.com/mailman/listinfo/fedora-selinux-list
Fedora security: fedoraproject.org/wiki/Security
SELinux reference policy: oss.tresys.com/projects/refpolicy

# Turning off SELinux

tip
There are two ways to disable SELinux: You can modify the /etc/selinux/config file so that it includes the line **SELINUX=disabled** and reboot the system, or you can use **system-config-selinux** (as explained on the next page).

If there is a chance you will want to enable SELinux in the future, putting SELinux in permissive mode is a better choice than disabling it. This strategy allows you to turn on SELinux more quickly when you decide to do so.

# config: The SELinux Configuration File

The /etc/selinux/config file, which has a link at /etc/sysconfig/selinux, controls the state of SELinux on the local system. Although you can modify this file, it may be more straightforward to work with **system-config-selinux** (as explained in the next section). In the following example, the policy is set to targeted, but that setting is of no consequence because SELinux is disabled.

```
```
$ cat /etc/selinux/config
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
# enforcing - SELinux security policy is enforced.
# permissive - SELinux prints warnings instead of enforcing.
# disabled - SELinux is fully disabled.
SELINUX=disabled
# SELINUXTYPE= type of policy in use. Possible values are:
# targeted - Only targeted network daemons are protected.
# strict - Full SELinux protection.
SELINUXTYPE=targeted
```
```