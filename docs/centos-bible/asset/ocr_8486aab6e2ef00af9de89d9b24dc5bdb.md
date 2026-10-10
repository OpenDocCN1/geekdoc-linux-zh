+   
+   - **SELinux Troubleshooter** — The SELinux Troubleshooter will start an icon in the desktop panel when SELinux detects something that violates SELinux policy. Click that icon to display the setroubleshoot browser window to see descriptions and potential fixes for the problem. You can also start the setroubleshoot browser directly by selecting Applications > System Tools > SELinux Troubleshooter.
+   

+   
+   - **SELinux Administration Window** — Open the SELinux Administration window (select System > Administration > SELinux Management) to change the status of SELinux (Enabled, Disabled, or Enforcing) or change the default policy type (targeted by default). You can also modify SELinux settings for users, files and directories, policy modules, and network ports.
+   

+   
+   - **SELinux Commands** — A set of command-line tools can be used to modify SELinux policies. These commands include `chcon` (to label files and directories) and `setsebool` (to turn on and off SELinux attributes). To get information on how specific daemons are being handled in SELinux, refer to various SELinux policy man pages (`fipd_selinux`, `httpd_selinux`, `kerberos_selinux`, `named_selinux`, `nfs_selinux`, `nis_selinux`, `rsysnd_selinux`, and `ypbind_selinux`).
+   

# Using SELinux in CentOS

If you use the targeted SELinux policy (which is delivered on and by default), you can still administer Linux as you always have. The following procedure describes the software packages you need to use SELinux and starts you off working with the default targeted policy. If you need additional information, visit http://selinuxproject.org/page/Main_Page to find a plethora of useful SELinux documentation.

# SELinux

Support for SELinux is built into the Linux 2.6 kernel. In fact, SELinux is on by default in the latest release of CentOS. If you prefer to have SELinux off, after you boot the desktop, you can open the SELinux Administration window (select System > Administration > SELinux Management) and set the "Enforcing Current" selection to Permissive. Permissive causes SELinux to check and note where SELinux would fail, but doesn't actually fail.

With SELinux enabled, you might also want the following software packages installed:

+   
+   - **checkpolicy** — Contains the SELinux policy compiler named `checkpolicy`. Use this package to build or check policies for SELinux. Using `checkpolicy`, you create binary policy files from policy configurations and parameters in a policy.conf file. (Type `man checkpolicy` to read about `checkpolicy`.)
+   - **libselinux** — Contains the application programming interface for SELinux applications. It includes components used by application programs to check SELinux status.
+