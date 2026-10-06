
## Tools in SELinux

Tools available with SELinux let you work with change policy settings in SELinux. Many of these tools come in the selinux-policy, selinux-policycoreutils and setroubleshoot-server packages in the current release of Fedora. Tools include the following:

- **SELinux Troubleshooter** — The SELinux Troubleshooter will start an icon in the desktop panel when SELinux detects something that violates SELinux policy. Click that icon to display the setroubleshoot browser window to see descriptions and potential fixes for the problem. You can also start setroubleshoot browser by directly selecting Applications → System Tools → SELinux Troubleshooter.

- **SELinux Policy Generation Tool** — Graphical tool for generating your SELinux policy framework. Application developers or systems administrators can use this tool to confine users or access only those resources they need.

- **SELinux Administration window** — Open the SELinux Administration window (select System → SELinux Management) to change the status of SELinux (enabled, disabled, or enforcing) or change the default policy type (targeted by default). You can also modify SELinux settings for users, files and directories, modules and network ports.

- **SELinux commands** — a set of command line tools can be used to modify SELinux policies. These commands include `chcon` (to label files and directories) and `setsebool` (to turn on and off SELinux attributes). To get information on how specific processes are being handled in SELinux, refer to various SELinux policy pages (fpid_selinux, http_selinux, kerberos_selinux, named_selinux, nfs_selinux, nis_selinux, rsync_selinux, and ybind_selinux).

## Using SELinux in Fedora and RHEL

If you used SELinux policy (which is delivered and on by default), you can still administer Linux as you as always have. The following procedure describes the software packages you need to use SELinux and starts you off with the default targeted policy. If you need additional information, refer to the following:

- **Red Hat Enterprise Linux 4 SELinux Guide** — Describes how to use, administer, and troubleshoot SELinux in Red Hat Enterprise 4. While some of the specific policy settings are different for the most recent Fedora, this is an excellent guide for understanding how SELinux works in RHEL and Fedora systems. You can find document at `http://www.redhat.com/docs/manuals/enterprise/RHEL-4-Manual/selinux-guide/`.

- **SELinux Documentation** — Most of documents that come in the selinux-doc package are standards-type documents from the U.S. National Security Agency (NSA). Look in `/usr/share/doc/selinux-doc` directory of your Fedora or RHEL system for files, using your Web browser or PDF viewer.

## Getting 10: Understanding System Administration 459

## Getting SELinux

Support for SELinux is built into the Linux 2.6 kernel. In fact, SELinux is on default in the latest release of Fedora. If you prefer SELinux off, after you boot the desktop, you can open the SELinux administration window (System -> Administration -> SELinux Management) and set the Enforcing Curve to Permissive. Permissive causes SELinux to check and note where SELinux would fail, but doesn't actually fail.

With SELinux, enabled might also allow the following software packages installed:

- **checkpolicy** — Contains the SELinux policy compiler named checkpolicy. Use this to build or check policies for SELinux. Using checkpolicy, you create binary files from policy configurations and parameters in a policy.conf file. (Type man policy to read about checkpolicy.)
- **libselinux** — Contains the programming interface for SELinux applications. It includes components used by application programs to keep SELinux status.
- **policycoreutils** — Contains basic utilities needed to operate an SELinux system. Commands include fixfiles (to check and possibly correct security attributes on file), restorecon (to set attributes for selected files), audit2allow (to translate messages from /var/log/messages to rules that SELinux can use), newrole (to open a shell in a new role), load_policy (to load a policy file), run_init (to run an init script using the correct context), sestatus (to check whether SELinux is currently enabled), and setfiles (to set the security contexts of files).
- **selinux-doc** — Contains a lot of SELinux documentation that is stored in the /usr/share/selinux directory.
- **selinux-policy-ms** — Contains the multi-level security translation table for SELinux.
- **selinux-targeted** — Contains the sample policy file used to incorporate the targeted policy into a running Linux system, as well as contexts and the booleans file to make run-time changes to SELinux.
- **setools** — Contains tools for managing parts of a running system that define access users have to different components of the Linux system.

## Checking whether SELinux

After Fedora RHEL is installed, you can check the /etc/selinux/config file (which is linked to /etc/sysconfig/selinux) to see if SELinux is enabled, and what policies are in effect. That file sets two critical variables for a Fedora system configured to be SELinux:

- **SELinux State** — The SELINUX variables set the state of SELinux. If you enable SELinux during Fedora installation this starts out as SELINUX=enforcing (which causes security policies for SELinux to be enforced). If SELinux is disabled for most practical purposes, if you use SELINUX you will want to enable the SELINUX policy (which is the default). While not locking down those daemon processes that are most critical to protect from attacks, Standard Linux default security protects everything else in the operating system.

You can override your default settings to lock SELinux into permissive mode from the Linux boot prompt by adding the following to the end of the kernel line from GRUB screen when you boot Fedora:

`setforce 0`

With SELinux in permissive mode (setforce 0), you can still log in and use the system, with potentially devastating permission failures simply resulting in error messages. If SELinux is in permissive, you may likewise return SELinux to enforcing mode from the boot prompt by typing setforce 1. You can change the SELinux state permanently, using the SELinux Administration window.

## Checking SELinux status

There are many tools for checking the status of SELinux on your Fedora System. To check whether or not SELinux is enabled, type the following:

```
sestatus
```

The output shows SELinux is enabled. If SELinux was set to permissive, the output would look more like:

```
SELinux status:                 disabled
SELinux's mount:                /selinux
Current mode:                   permissive
Policy from config:             targeted
Policy version:                 2
Process contexts:               user_u:unconfined_r:unconfined_t:s0-s0:c0:01223
```

## Chapter 10: Understanding System Administration 461

```
File contexts:
Controlling term: user_u:unconfined_r:devpts_t
/etc/passwd: user_u:unconfined_r:etc_t
/etc/shadow: user_u:unconfined_r:shadow_t
/bin/bash: user_u:unconfined_r:shell_t
/bin/login: user_u:unconfined_r:login_t
/bin/sh: user_u:unconfined_r:bin_t
/sbin/getty: user_u:unconfined_r:getty_t
/sbin/init: system_r:init_t
/sbin/sshd: user_u:unconfined_r:getty_t
/lib/Libc.6: system_r:shd_t
/lib/ld-linux.so.2: system_r:lib
```

Press the Spacebar to go through the output. Beside how SELinux is enabled and in enforcing mode, this output shows the processes and file contexts that to see and change basic SELinux settings from a graphical interface, you can open the SELinux Administration window. From the GNOME Desktop, select Administration SELinux Management. From that window, you can set whether SELinux is Disabled, Enforcing, or Permissive. You can also set the SELinux policy to use (targeted).

Changing the policy type or turning the SELinux service from off to on requires you to relabel the file system. Changing policy should never be done lightly. If you decide to change policy through the SELinux Administration window, that change also requires that the file system be relabeled. By changing the policy through this window, the file system will be relabeled automatically the next time you reboot your computer (or you can check the box to prevent relabeling the file system on the next reboot).

> NOTE: Relabeling the file system can be a long and time-consuming activity. Again, remember that changing policies is a major change to your operating system. The more nodes there are in your file system, the longer it will to relabel your file system the next time you boot your computer.

You can check the security context in which you are using the id command with the -z option. The following example shows that your current context is the root user, your system_r role, and the type is unconfined_t.

```
# id -Z
unconfined_u:unconfined_r:unconfined_t:s0-s0:c0:01223
```

SELinux is capable of turning off a lot of error messages. By default, messages are directed to the /var/log/messages file. Because the file contains messages from many
