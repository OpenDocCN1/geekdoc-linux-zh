
Listing setup files
find / -perm -4000 -exec ls -lh {} \; 2> /dev/null
-rwS--x-x-x,1 root root 30K Oct 5 12:10 /usr/sbin/userhelper
-r-S-s-x---,1 root apache 11K Aug 21 07:15 /usr/sbin/suexec
-rws---x-x-,1 root root 1.9M Oct 4 21:38 /usr/sbin/Xorg
-rws---x-x,1 root root 15K Oct 5 08:28 /usr/bin/chsh
-rwsr-xr-x,1 root root 23K Sep 14 05:14 /usr/bin/passwd
-rws---x-x,1 root root 16K Oct 5 08:24 /usr/bin/cfin
---S---x-x,2 root root 169K Aug 21 04:24 /usr/bin/sudoedit
-rwsr-sf-x,1 root root 45K Aug 21 03:26 /usr/bin/crontab
----S-x-x,2 root root 169K Aug 21 04:24 /usr/bin/sudo
-rwsr-xf-x,1 root root 60K Sep 7 08:04 /usr/bin/gpasswd
-rwsr-xr-x,1 root root 51K Sep 29 11:58 /usr/bin/at

This command uses find to locate all files that have their setup bit set (mode 4000). The hyphen preceding the mode causes find to report on any file that has this bit set, regardless of how the other bits are set. The output sent to standard error is redirected to /dev/null so that it does not clutter the screen.

You can also set up a program, such as AIDE (Advanced Intrusion Detection Environment; part of the aide package), that will take a snapshot of the system and check it periodically. See sourceforge.net/projects/aide for more information.

## GETTING HELP

The Fedora/RHEL distribution comes with extensive documentation (page 124). Red Hat maintains a Web page that points you toward many useful support documents: www.redhat.com/apps/support. Links to many other sources of assistance can be found at fedoraproject.org/en/get-help. Fedora maintains documents at docs.fedoraproject.org. You can also find help on the System Administrators Guild site (www.sage.org). The Internet is another rich source of information on managing a Linux system; refer to Appendix B (page 1033) and to the author’s home page (www.sobell.com) for pointers to useful sites.

You do not need to act as a Fedora/RHEL system administrator in isolation; a large community of Linux/Fedora/RHEL experts is willing to assist you in getting the most out of your system, although you will get better help if you have already tried to solve a problem yourself by reading the available documentation. If you are unable to solve a problem by consulting the documentation, a well-thought-out question posed to the appropriate newsgroup, such as comp.os.linux.misc, or mailing list can often generate useful information. Be sure you describe the problem accurately and identify your system carefully. Include information about your version of Fedora/RHEL and any software packages and hardware that you think relate to the problem. The newsgroup comp.os.linux.answers contains postings of solutions to common problems and periodic listings of the most up-to-date versions of FAQs and HOWTO documents. See www.cats.org/ ~esr/faqs/smart-questions.html for a helpful paper by Eric S. Raymond and Rick Moe titled “How to Ask Questions the Smart Way.”

## SELINUX

Traditional Linux security, called *Discretionary Access Control* (DAC), is based on users and groups. Because a process run by a user has access to anything the user has access to, fine-grained access control is difficult to achieve. Fine-grained access control is particularly important on servers, which often hold programs that require root privileges to run.

SELinux (Security Enhanced Linux), which was developed by the U.S. National Security Agency (NSA), implements *Mandatory Access Control* (MAC) in the Linux kernel. MAC enforces security policies that limit what a user or program can do. It defines a security policy that controls some or all objects, such as files, devices, sockets, and ports, and some or all subjects, such as processes. Using SELinux, you can grant a process only those permissions it needs to be functional, following the principle of least privilege (page 466). MAC is an important tool for limiting security threats that come from user errors, software flaws, and malicious users. The kernel checks MAC rules after it checks DAC rules.

SELinux can be in one of three states (modes):

- **Enforcing**—The default state, wherein SELinux security policy is enforced. No user or program will be able to do anything not permitted by the security policy.
- **Permissive**—The diagnostic state, wherein SELinux sends warning messages to a log but does not enforce the security policy. You can use the log to build a security policy that matches your requirements.
- **Disabled**—SELinux does not enforce a security policy because no policy is loaded.

Running SELinux in permissive or enforcing state degrades system performance somewhat. Although SELinux usually does not provide benefit on a single-user system, you may want to consider using SELinux on a server that connects to the Internet. If you are unsure whether to use SELinux, selecting permissive state allows you to easily change to disabled or enforcing state at a later date.

SELinux implements one of the following policies:

- **Targeted**—Applies SELinux MAC controls only to certain (targeted) processes (default).
- **MLS**—Multilevel Security protection.
- **Strict**—Applies SELinux MAC controls to all processes (*RHEL*).

This section discusses the targeted policy. With such a policy, daemons and system processes that do not have a specified policy are controlled by traditional Linux DACs. With the strict policy, all processes are controlled by SELinux (MACs). Setting up a system that runs under strict policy is beyond the scope of this book.

There is always a tradeoff between security and usability. The targeted policy is less secure than the strict policy, but it is much easier to maintain. When you run the strict policy, you will likely have to customize the policy so that users can do their work and the system can function appropriately.

You can switch from one policy to the other (as explained shortly). Despite this flexibility, it is not a good idea to switch from a targeted to a strict policy on a production system. If you do so, some users may not be able to do their work. You would need to customize the policy in such a case. Changing from a strict to a targeted policy should not create any problems.

### More Information

- Web NSA: www.nsa.gov/research/selinux
- Fedora SELinux wiki: fedoraproject.org/wiki/SELinux
- SELinux News: selinuxnews.org
- SELinux for distributions (Sourceforge): selinux.sourceforge.net
- Fedora SELinux mailing list: www.redhat.com/mailman/listinfo/fedora-selinux-list
- Fedora security: fedoraproject.org/wiki/Security
- SELinux reference policy: oss.tresys.com/projects/refpolicy

### Turning off SELinux

Tip
There are two ways to disable SELinux: You can modify the /etc/selinux/config file so that it includes the line **SELINUX=disabled** and reboot the system, or you can use **system-config-selinux** (as explained on the next page).

If there is a chance you will want to enable SELinux in the future, putting SELinux in permissive mode is a better choice than disabling it. This strategy allows you to turn on SELinux more quickly when you decide to do so.

### config: The SELinux Configuration File

The /etc/selinux/config file, which has a link at /etc/sysconfig/selinux, controls the state of SELinux on the local system. Although you can modify this file, it may be more straightforward to work with **system-config-selinux** (as explained in the next section). In the following example, the policy is set to targeted, but that setting is of no consequence because SELinux is disabled.

```bash
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
