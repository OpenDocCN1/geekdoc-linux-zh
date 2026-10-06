# CHAPTER 8 Operating System Hardening

To do this, edit the /etc/rc.dc.local file and place # in front of the following lines, as shown:

```
# This will overwrite /etc/issue at every boot. So, make any changes
# want to make to /etc/issue or you will lose them when you reboot.
#echo "$S" > /etc/issue
#echo "$S" >> /etc/issue
#echo "Kernel $(uname -r) on $a $(uname -m)" >>/etc/issue
#
#cp -f /etc/issue /etc/issue.net
#echo >> /etc/issue
```

Remove the following files: "issue.net" and "issue" under /etc/ directory:
[root@kapil]# rm -f /etc/issue
[root@kapil]# rm -f /etc/issue

In general, security concepts apply regardless of operating system. However, truly hardening an operating system requires a certain level of expertise with that particular system.

The following websites provide information useful for helping you secure your Linux server:

+   - Linux Security Administrators Guide: www.linuxsecurity.com/docs/SecurityAdminGuide/SecurityAdminGuide.html

+   - Linux.com: www.linux.com/

> FYI: Patch Conflicts
A patch could possibly conflict with some software or settings on your system. To avoid these conflicts, you should first apply patches to a test machine to ensure no conflicts exist before you apply them to production machines.

# Patching the Operating System

From time to time, security flaws are found in operating systems. As software vendors become aware of flaws, they usually write corrections to their code, known as patches or updates. Whatever operating system you use, you must apply these patches as a matter of routine. Windows patches are probably the most well-known, but patches can be released for any operating system. You should patch your system any time a critical patch is released. You might consider scheduling a specific time to update patches. Some organizations find updating once per quarter or per month is necessary.

For Windows you can go to www.microsoft.com. On the left-hand side you should notice a link that says Updates. If you click on it, you can scan your machine for missing patches and download them from the website. Red Hat offers a similar service for Red Hat Linux users. On the website www.redhat.com/security/, users can scan for updates.