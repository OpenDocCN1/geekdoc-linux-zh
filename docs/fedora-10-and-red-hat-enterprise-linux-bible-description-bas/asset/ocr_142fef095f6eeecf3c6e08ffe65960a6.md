For most practical purposes, if you use SELINUX you will want to enable the SELINUX policy (which is the default). While not locking down those daemon processes that are most critical to protect from attacks, Standard Linux default security protects everything else in the operating system.

You can override your default settings to lock SELinux into permissive mode from the Linux boot prompt by adding the following to the end of the kernel line from GRUB screen when you boot Fedora:

setforce 0

With SELinux in permissive mode (setforce 0), you can still log in and use the system, with potentially devastating permission failures simply resulting in error messages. If SELinux is in permissive, you may likewise return SELinux to enforcing mode from the boot prompt by typing setforce 1. You can change the SELinux state permanently, using the SELinux Administration window.

# Checking SELinux status

There are many tools for checking the status of SELinux on your Fedora System. To check whether or not SELinux is enabled, type the following:

```
# sestatus -v | less
SELinux status:                                 disabled
```

The output shows that SELinux is not enforced on the current system. If SELinux was set to permissive, the output would look more like the following:

SELinux status:                 enabled
SELinux's mount:                /selinux
Current mode:                   enforcing
Mode from config file:          enforcing
Policy version:                 22
Policy from config file:        targeted

Process contexts:
Current context:                user_u:system_r:unconfined_t:SystemLow-SystemHigh
Init context:                   system_u:system_r:init_t
/sbin/getty                    system_u:system_r:getty_t
/usr/sbin/sshd                  system_u:system_r:unconfined_t:SystemLow-SystemHigh