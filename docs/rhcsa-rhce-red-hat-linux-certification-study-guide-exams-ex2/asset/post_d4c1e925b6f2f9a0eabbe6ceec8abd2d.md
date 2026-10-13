
# FIGURE 4-12

One SELinux alert

## Summary

SELinux is preventing /usr/bin/sudo "setuid" access.

## Detailed Description

SELinux denied access requested by sudo. It is not expected that this access is required by sudo and this access may signal an intrusion attempt. It is also possible that the specific version or configuration of the application is causing it to require additional access.

## Allowing Access

You can generate a local policy module to allow this access - see FAQ (http://docs.fedoraproject.org/selinux-faq/fc5/#id2961385). Please file a bug report.

## Additional Information

| Field | Value |
|---|---|
| Source Context | user_u:user_r:user_t:s0 |
| Target Context | user_u:user_r:user_t:s0 |
| Target Objects | None [ capability ] |
| Source | sudo |
| Source Path | /usr/bin/sudo |
| Port | <Unknown> |
| Host | <unknown> |
| Source RPM Packages | sudo-1.7.2p2-9.el6 |
| Target RPM Packages | |
| Policy RPM | selinux-policy-3.7.19-54.el6_0.3 |
| SELinux Enabled | True |
| Policy Type | targeted |
| Enforcing Mode | Enforcing |
| Plugin Name | catchall |
| Host Name | Maui |
| Platform | Linux Maui 2.6.32-71.7.1.el6.x86_64 #1 SMP Wed Oct 27 03:44:59 EDT 2010 x86_64 x86_64 |
| Alert Count | 13 |
| First Seen | Tue Dec 21 20:52:00 2010 |
| Last Seen | Wed Dec 22 09:03:57 2010 |
| Local ID | 02a40edf-9dfb-40f7-9841-56a143286f86 |

# SELinux Boolean Issues

After deactivating the allow_user_exec_content boolean described earlier, I created a simple script named script1 for a user governed by the user_u label. After making that script executable, I tried running it with the /home/examprep/script1 command. Even though that user had ownership of the file, with executable permissions set, that attempt led to the following message:

```
-bash: /home/examprep/script1: Permission denied
```

That led to the log excerpt shown in Figure 4-13. Note the Fix Command section; it explicitly cites the command required to address the problem. As an administrator, you need to decide whether such users should be given the ability to execute their own scripts. If so, then the noted command would address the problem.

# The GUI SELinux Management Tool

If you've taken the time to learn SELinux from the command line, this section should be just a review. For many users, the easiest way to change SELinux settings is with the SELinux Administration tool, which you can start with the system-config-selinux command. As shown in Figure 4-14, it starts with a basic view of the status of SELinux on the local system, reflecting some of the information shown in the output to the sestatus command.

> exam watch
> To install the GUI SELinux Management tool, run the yum install policycoreutils-gui command. In this case, there is no system-config-selinux package.

# FIGURE 4-13

A SELinux alert and a solution

```
Summary:
SELinux is preventing /bin/bash "execute" access on script1.

Detailed Description:

SELinux denied access requested by bash. The current boolean settings do not allow this access. If you have not setup bash to require this access this may signal an intrusion attempt. If you do intend this access you need to change the booleans on this system to allow the access.

Allowing Access:

Confined processes can be configured to run requiring different access, SELinux provides booleans to allow you to turn on/off access as needed. The boolean allow_user_exec_content is set incorrectly.
Boolean Description:
allow_user_exec_content

Fix Command:

# setsebool -P allow_user_exec_content 1
```

# FIGURE 4-14

SELinux Status in the Administration tool

![](img/9139201cfcaf4292284a0eed074928e5_243_0.png)

The SELinux Management tool is much more capable than the previous utility that was part of the Security Level Configuration tool. As you can see, there are options for Default and Current Enforcing Modes, which you can set to Enforcing, Permissive, or Disabled. While the focus of SELinux is on a Targeted policy, MLS is also available. Generally, you don't need to activate the Relabel On Next Reboot option unless you've changed the default policy type.

There are a number of categories shown in the left pane of the SELinux Management Tool window described in the following sections. In the RHCE half of this book, you'll revisit this tool with more of a focus on Boolean settings in the second half of this book.

# SELinux Boolean Settings

In the SELinux Administration tool, click Boolean in the left-hand pane. Scroll through available modules. As you can see, SELinux policy can be modified in a number of different categories, some related to administrative functions, others to specific services. A select number of these options are shown in Figure 4-15. Any changes you make are reflected in boolean variables in the /selinux/booleans directory. Module categories of interest for the RHCSA exam include cron, init, mount, qemu, and that catch-all category: unknown. As the list is relatively short, the associated booleans are listed in Table 4-9. The booleans appear in the order shown in the SELinux Management tool.

# File Labeling

You can change the default labels associated with files, some of which are described earlier in this chapter (and in other chapters discussing SELinux contexts). Some of the options are shown in Figure 4-16. Any changes to this screen are written to the file_contexts.local file in the /etc/selinux/targeted/contexts/files directory.

# User Mapping

The User Mapping section allows you to go beyond the defaults for regular and administrative users. The display here illustrates the current output to the semanage login -l command. If you don't remember the intricacies of the semanage command, it may be easier to use this screen to map existing users to different maps. Click Add to open the Add User Mapping window shown in Figure 4-17. That figure also illustrates how you might reclassify a user named michael as a SELinux user_u user type.

# SELinux User

The SELinux User section allows you to specify and modify default roles for standard users, such as regular users (user_u), system users (system_u), unconfined users (unconfined_u), and the administrative root user.

# Network Port

The Network Port section associates standard ports with services, which will be important in the RHCE section of this book.

## TABLE 4-9 Selected SELinux Boolean Options

| Boolean | Description |
|---|---|
| fcron_crond | Supports fcron rules for job scheduling |
| cron_can_relabel | Allows cron jobs to change the SELinux file context label |
| allow_daemons_use_tty | Lets service daemons use terminals as needed |
| allow_daemons_dump_core | Supports writing of core files to the top-level root directory |
| init_upstart | Allows supplanting of SysVInit with upstart |
| allow_mount_anyfile | Permits the use of the mount command on any file |
| qemu_use_nfs | Supports the use of NFS filesystems for virtual machines |
| qemu_use_usb | Supports the use of USB devices for virtual machines |
| qemu_full_network | Supports networking for virtual machines |
| qemu_use_cifs | Supports the use of CIFS (Common Internet File System) filesystems for virtual machines |
| qemu_use_comm | Supports a connection for virtual machines to serial and parallel ports |
| allow_sysadm_exec_content | Allows sysadm_u users the right to execute scripts |
| allow_xguest_exec_content | Allows xguest_u users the right to execute scripts |
| allow_user_exec_content | Allows user_u users the right to execute scripts |
| allow_staff_exec_content | Allows staff_u users the right to execute scripts |
| allow_guest_exec_content | Allows guest_u users the right to execute scripts |

# FIGURE 4-15

Booleans in the SELinux Management tool

![](img/9139201cfcaf4292284a0eed074928e5_244_0.png)

# FIGURE 4-16

File types in the SELinux Management tool.

![](img/9139201cfcaf4292284a0eed074928e5_246_0.png)

# FIGURE 4-17

Map a user in the SELinux Management tool.

![](img/9139201cfcaf4292284a0eed074928e5_246_1.png)
