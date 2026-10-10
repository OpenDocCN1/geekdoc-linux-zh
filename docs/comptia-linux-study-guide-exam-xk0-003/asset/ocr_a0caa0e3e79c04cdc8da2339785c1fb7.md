Apache-related files only. Thus, if a bug exists in Apache, the server’s context limits the damage that Apache can do, either accidentally or if the bug is abused by a cracker. The Apache context is unlikely to grant it access to /etc/passwd, for instance.
SELinux requires support in the Linux kernel and in many programs and support tools outside of the kernel. If you want to use it, you should first ensure that your kernel includes SELinux support. You can then install relevant SELinux packages, whose names are likely to start with the string selinux. You may need to install several packages, including one or more policy packages, which include the rules that define MACs, domains, contexts, and so on, to make a working SELinux system.

![](bbox=[0.14, 0.3, 0.23, 0.36])

> SELinux can be confusing, in part because it reuses so many terms. MAC can also refer to media access control, a type of low-level network address; and the word domain is used in many other network contexts, such as the Domain Name System (DNS) or a Microsoft Windows domain.

In practice, SELinux can be very complex and confusing. It also degrades the system’s performance slightly because the kernel must perform additional security checks. If the default policies provided with your distribution aren’t suitable for your installation, you’ll have a hard time modifying them—and this task is complex enough that I can’t cover it in this book. (The Linux+ exam also doesn’t cover SELinux policy configuration.)

# ## Configuring SELinux Running Modes

Once an SELinux kernel is running and the support tools are installed, SELinux will run in one of three modes:

+   * **Disabled** The SELinux extensions are turned off completely.
+   * **Permissive** The SELinux extensions are turned on enough to log results, but the system doesn’t actually restrict users’ actions. This can be a good mode for testing your SELinux configuration prior to bringing a system completely online.
+   * **Enabled** The SELinux extensions are fully operational, restricting accesses based on your SELinux policies.

You can switch your SELinux modes in several ways. One is to use the /selinux/enforce file, which is part of an SELinux-specific virtual filesystem (/selinux). You can store a value of 0 or 1 in this file to switch between permissive and enabled modes, respectively:

```
`# echo 1 > /selinux/enforce`
```

![](bbox=[0.14, 0.92, 0.23, 0.98])

> If SELinux is enabled, you’ll need to be in the sysadm_r role to modify files in /selinux. You can use the newrole command to switch roles, as in newrole -r sysadm_r.