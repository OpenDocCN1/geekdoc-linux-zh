method, which involves the sysinit script and a set of directories that contain links to the system's services, each representing a runlevel.

Red Hat and Debian use a similar structure for these directories, with one main difference. Red Hat's tree structure is shown on the left, with Debian on the right:

+   Red Hat
+   /etc/rc.d
+   * init.d
+   * rc0.d
+   * rc1.d
+   * rc2.d
+   * rc3.d
+   * rc4.d
+   * rc5.d
+   * rc6.d
+   Debian
+   /etc/
+   * init.d
+   * rc0.d
+   * rc1.d
+   * rc2.d
+   * rc3.d
+   * rc4.d
+   * rc5.d
+   * rc6.d

The init.d directory in each case contains all the configured daemon executables. These are linked to from the runlevel directories by two types of scripts—start and kill scripts. Both scripts are symlinks to the daemon executables in the init.d directory.

Start scripts look like s24rpcnc1a, where the presence of the capital s signals the daemon to start itself, the numerals force a particular start order, and the name of the service is the last piece of the link name as a mnemonic.

Kill scripts use the same naming convention, with a capital k instead of an s. The presence of the capital k signals the daemon to gracefully turn itself off.

After the system initialization is finished, the init process reads the /etc/inittab file and the line that sets the default runlevel value. After that value is obtained, the init process finds the appropriate runlevel directory and, upon entering it, runs the start scripts in number order (0–99).

When the runlevel is changed, the system takes note of the state of the current runlevel's daemons, inspects the target runlevel's scripts, and leaves those that are defined with an s symlink running. If no s symlink exists in the target runlevel for a daemon, it's considered undefined and the k script to terminate that daemon is run before the runlevel is changed.

> The use of .pid files in the /var/run or /var/lock/subsys directories helps the system determine what's running and the state of those daemons. This is not particularly relevant to the exam, but a good sysadmin should read more about it, starting with the init man pages.