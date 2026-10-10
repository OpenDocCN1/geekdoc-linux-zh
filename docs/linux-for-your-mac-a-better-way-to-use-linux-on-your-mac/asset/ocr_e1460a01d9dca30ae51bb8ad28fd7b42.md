However, you may want to make a backup copy of the current modules (which is found under the `/lib/modules/2.x.x` directory, where `x.x` represents the version of your Linux kernel).

To use your new kernel, copy the file `system.map` to the `/boot` directory. You can also copy `vmlinux` to the `/boot` directory. However, BootX and yaBOOT users will then need to copy `vmlinuz` to the appropriate Mac OS System Folder, and change BootX or yaBOOT's configuration file to use the new kernel.

# # Resources

+   * http://www.redhat.com. Home page for the Intel- and Alpha-based Linux distributions.
+   * http://www.yellowdoglinux.com. Home page for Yellow Dog Linux, with links to documentation on related system tools.
+   * http://www.linuxppc.com. Distributor of LinuxPPC 2000, and a good place to check for errata, bug fixes, and updates.
+   * http://www.suse.com. Home page for SuSE Linux, with links to troubleshooting, and a hardware compatibility database. You will also find links to updated software packages.
+   * http://www.rpm.org. An open source Web site devoted to promoting RPM technology. While there, make sure to download a copy of Ed Bailey's classic tome, “Maximum RPM.” You will benefit from reading about RPM.
+   * http://www.cis.ohio-state.edu/~rowland/projects/OpenSource/security-basics/security-basics/index.html. A great site for basic security tips when using Linux.
+   * http://www.kernel.org. The definitive Web site for the latest version of the Linux kernel.
+   * http://www.eecs.udel.edu/~mills/ntp/clock1.htm. A listing of public-access time servers on the Internet. This will help keep your system running on time.
+   * http://www.erlenstar.demon.co.uk/unix/faq_2.html#SEC14. Answers questions like “What is a zombie?”
+   * http://www.solucoop.orge.ca/linuxconf/. Home page for the `linuxconf` client.
+   * http://ctdp.tripod.com/os/linux/howlinuxworks/linux_hlprocess.html. A great page outlining how Linux process management works.