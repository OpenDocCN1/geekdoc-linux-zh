> **exam watch**
> Always remember to make sure that a service will be active after a reboot. The `chkconfig servicename on` command is one way to do this for xinetd services. Otherwise, anything you configure may not work after a system is rebooted.

There are two ways to activate an xinetd service. You can edit the configuration file directly by changing the `disable` field from `no` to `yes`. Then make the xinetd daemon reread the configuration files with the `service xinetd reload` command.

Alternatively, you can use the `chkconfig servicename on` command, which automatically makes this change and makes xinetd reread the configuration file.

# EXERCISE 10-1

# Configure xinetd

In this exercise, you will enable the Telnet service using xinetd. This exercise assumes that the telnet-server package is already installed. Before starting this exercise, try to establish a Telnet session using the command `telnet localhost`. If you're successful, Telnet was previously enabled; in that case, disable it first with the `chkconfig telnet off` command.

+   1. Edit `/etc/xinetd.d/telnet` and change the value of `disable` from `yes` to `no`.
+   2. Tell xinetd to reread its configuration file using this command:
+      ```
+      # service xinetd reload
+      ```
+   3. Try the `telnet localhost` command again. It should work.
+   4. Try to log in with an incorrect username or password.
+   5. Log in to another terminal. What do you see when you run `utmpdump /var/log/wtmp`?
+   6. Now log in with a correct username and password.
+   7. What do you see in `/var/log/messages`?
+   8. Log out of the Telnet session. What do you see now in `/var/log/messages`?
+   9. Use the `chkconfig` command to disable Telnet. (Remember that the name of the service is telnet.) Try connecting to the Telnet server again. Do you have to restart or reload xinetd?
+   10. What happens when you use `chkconfig` to disable Telnet? Does it change the `/etc/xinetd.d/telnet` configuration file?