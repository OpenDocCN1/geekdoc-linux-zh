6. Next on Red Hat-like systems, you can use the authconfig-tui utility to configure the other user information and authentication settings. Launch the tool from the command line and select Use Winbind over User Information. Select Use Winbind Authentication under Authentication, select Next, and finally select OK to save your settings.

7. On Linux distributions using systemd as the service manager, you can start the winbind daemon using the systemctl command:

```
[root@fedora-server ~]# systemctl start winbind
```

On versions (pre-systemd) of Debian-based distros, you can start the daemon by executing this command:

```
ubuntu-server:-$ sudo /etc/init.d/winbind start
```

8. Use the wbininfo utility (provided with the samba-winbind-clients*.rpm package) to list all users in the Windows domain to make sure that things are working properly:

```
# wbinfo -u
```

That's it. The Linux server will now be able to consult and query the Windows Server for your user authentication needs.

# Troubleshooting Samba

The following are a few solutions to simple problems you might encounter with Samba:

+   * Restart Samba. This might be necessary because either Samba has entered an undefined state or (more likely) you've made major changes to the configuration but forgot to reload Samba so that the changes effect.

+   * Make sure the configuration options are correct. Errors in the smb.conf file are typically in directories, usernames, network numbers, and hostnames. A common mistake occurs when a new client is added to a group that has special access to the server, but Samba isn't told the name of the new client being added. Don't forget that syntax-type errors, the testparm utility is your ally.

+   * Log files. Samba can be configured to generate as few as many logs as you want, and with varying levels of detail. The log files are your friend when troubleshooting Samba issues. Red Hat-like distros such as Fedora Samba-specific log files under the /var/log/samba/ directory. Keep a watchful eye on the logs!