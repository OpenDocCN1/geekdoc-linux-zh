+   * runlevel 2  This traditionally means normal multiuser state, except no NFS or other networking services are run. Basically, it is a state where you can access the network, but others can't access your services.
+   * runlevel 3  This is the normal multiuser mode—all system and network services that are configured are started. This is the normal runlevel for systems not running X logins.
+   * runlevel 4  This is an undefined state. OpenLinux treats this exactly as level 3.
+   * runlevel 5  Multiuser plus X Display Manager—all configured system and network services are run. Additionally, the xdm or kdm program is started to allow X logins from the console (and possibly remotely, depending on setup).
+   * runlevel 6  This is the runlevel a system goes to when it is rebooted.
+   * runlevel s/S  This is another name generally for single-user mode.

The /etc/inittab file controls how or whether each of these runlevels is entered. This controls the very early portion of the boot process. It generally tells init to run a few crucial programs; then it tells init what the default runlevel will be. (It also holds configuration information for the programs that control the Linux console (getty). In OpenLinux, your default runlevel is likely to be 5, unless you haven't set up X, in which case it should be 3.

After all the kernel setup is done, init switches into its default runlevel and starts up the daemons that should run there. This process is controlled by files under the /etc/rc.d/ directory. Basically, for every runlevel there is an rcN.d directory, where N is equal to the runlevel number. So all the files in /etc/rc.d/rc3.d/ would be run when the system goes to runlevel 3.

In fact, it's all a bit more complicated than this. (Somehow you just knew that, didn't you?) The actual control files for the daemons reside in /etc/rc.d/init.d/. The files in the various rcN.d directories are actually symbolic links back to the files in /etc/rc.d/init.d/ so that init can be cued on which order to start things and whether to start or stop things at all. Here is an example—the listing of the /etc/rc.d/rc2.d/ directory:

![](bbox=[0.08, 0.77, 0.92, 0.86])