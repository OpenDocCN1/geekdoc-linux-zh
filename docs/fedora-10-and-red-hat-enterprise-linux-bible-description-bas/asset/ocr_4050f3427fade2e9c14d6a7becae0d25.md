# Tools in SELinux

Tools available with SELinux let you work with change policy settings in SELinux. Many of these tools come in the selinux-policy, selinux-policycoreutils and setroubleshoot-server packages in the current release of Fedora. Tools include the following:

+   * **SELinux Troubleshooter** — The SELinux Troubleshooter will start an icon in the desktop panel when SELinux detects something that violates SELinux policy. Click that icon to display the setroubleshoot browser window to see descriptions and potential fixes for the problem. You can also start setroubleshoot browser by directly selecting Applications → System Tools → SELinux Troubleshooter.

+   * **SELinux Policy Generation Tool** — Graphical tool for generating your SELinux policy framework. Application developers or systems administrators can use this tool to confine users or access only those resources they need.

+   * **SELinux Administration window** — Open the SELinux Administration window (select System → SELinux Management) to change the status of SELinux (enabled, disabled, or enforcing) or change the default policy type (targeted by default). You can also modify SELinux settings for users, files and directories, modules and network ports.

+   * **SELinux commands** — A set of command line tools can be used to modify SELinux policies. These commands include `chcon` (to label files and directories) and `setsebool` (to turn on and off SELinux attributes). To get information on how specific processes are being handled in SELinux, refer to various SELinux policy pages (fpid_selinux, http_selinux, kerberos_selinux, named_selinux, nfs_selinux, nis_selinux, rsync_selinux, and ybind_selinux).

# Using SELinux in Fedora and RHEL

If you used SELinux policy (which is delivered and on by default), you can still administer Linux as you as you always have. The following procedure describes the software packages you need to use SELinux and starts you off with the default targeted policy. If you need additional information, refer to the following:

+   * **Red Hat Enterprise Linux 4 SELinux Guide** — Describes how to use, administer, and troubleshoot SELinux in Red Hat Enterprise 4. While some of the specific policy settings are different for the most recent Fedora, this is an excellent guide for understanding how SELinux works in RHEL and Fedora systems. You can find document at `http://www.redhat.com/docs/manuals/enterprise/RHEL-4-Manual/selinux-guide/`.

+   * **SELinux Documentation** — Most of documents that come in the selinux-doc package are standards-type documents from the U.S. National Security Agency (NSA). Look in `/usr/share/doc/selinux-doc` directory of your Fedora or RHEL system for files, using your Web browser or PDF viewer.