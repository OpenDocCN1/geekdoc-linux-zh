# # Some Troubleshooting Tips

If the NIS software isn't behaving as you think it should, you can check a few things:

+   * Make sure the processes are running. Use `ps aux` to list all the running processes. Make sure you see the appropriate processes running, regardless of whether the machine is a client, a server, or both.
+   * Check system logs (in `/var/log`) to see if there are any messages indicating peripheral problems that could be affecting your configuration.
+   * If the processes appear to be running but are not responsive, kill them and restart them. In some rare circumstances, the daemon may be misbehaving and may need to be restarted.
+   * Make sure `/etc/nsswitch.conf` is configured properly. This is a common problem.
+   * If you are trying to start the daemons by hand, make sure you are logged in as `root`.

When encountering problems, slow down, take a short break, and then retrace your steps. It's amazing how often simply slowing down helps you find problems.

# ## Summary

This chapter covered the installation and configuration of NIS master servers, secondary servers, and clients. In addition to the setup of NIS itself, common “NISisms” and netgroups were discussed. The lessons learned from these sections put a powerful tool in your hands.

Some key points to remember:

+   * Use `ypinit` to set up NIS master servers and secondary servers.
+   * The `/var/yp` directory contains the makefile necessary to update NIS information.
+   * Consider separating NIS files from your regular system files for clarity.
+   * NIS servers need the `ypserv` daemon.
+   * NIS clients need the `ypbind` daemon.
+   * `yppasswd` allows users on NIS clients to change their passwords.
+   * Schedule a reboot to test all your changes.

Although it isn’t the most exciting feature to come along in recent history, NIS is one of the most useful of the core network services. In conjunction with other services, NIS gives you the ability to create a seamless system for all of your users.