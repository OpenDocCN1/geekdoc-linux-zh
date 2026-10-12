will) have more shared volumes by configuring them in the `AppleVolumes.default` file.

+   **6. Securing shared volumes** — Netatalk can take advantage of Linux security features to protect shared volumes. You can secure volumes at the host, user, and file and directory level.

+   **7. Share printers (/etc/atalk/papd.conf file)** — Netatalk can share any printer you have connected to Linux (or otherwise configured locally) by adding a definition to the `papd.conf` file. No printers are shared until you add them.

As you work with your shared volumes and printers, you will find that maintenance issues arise from time to time. In particular, you should refer to the following sections: “File- and directory-level security” (for dealing with hidden attribute files and directories), “Sharing files with netatalk and Samba” (to share the same directories from netatalk and Samba), and “Troubleshooting netatalk” (for general troubleshooting tips).

# # Starting netatalk

Start up netatalk as you would most Linux network services: from a start-up script. The netatalk script is called atalk (`/etc/init.d/atalk`). To turn it on, type the following as root user:

```
# chkconfig atalk on
```

The previous command causes netatalk to start the next time you reboot. To start it now, type:

```
# service atalk start
```

Here's what happens when you start the AppleTalk service:

+   * The AppleTalk daemon (atalkd) starts from the contents of the `/etc/atalk/atalkd.conf` file.
+   * The papd daemon registers print services using the contents of the `/etc/atalk/papd.conf` file.
+   * The afd daemon registers volumes from the contents of the `/etc/atalk/AppleVolumes.default` file (using settings from the `AppleVolumes.system` file).

To check that the netatalk service started properly, as root user type the following from any Linux system on the network (the output may take a minute or two to appear):

```
$ nbplookup

toys:APFServer       65280.115:128
toys:netatalk        65280.115:4
toys:Workstation     65280.115:4
```