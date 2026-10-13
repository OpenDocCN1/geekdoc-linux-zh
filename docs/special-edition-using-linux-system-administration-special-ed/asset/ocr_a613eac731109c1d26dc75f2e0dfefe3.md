# # Useful Scripts

The following are three useful scripts for managing your system’s processes and daemons:

+   - **chkdaemon**: Checks if a daemon is running and restarts it if it has stopped.
+   - **chkload**: Checks if the system load gets too high and if it crosses a threshold, alerts the administrator.
+   - **chkswap**: Checks the amount of swap space available and if it drops below a threshold, alerts the administrator.

# chkdaemon

The following script can be used to check if a daemon is running; if it isn’t it will restart the daemon. Create this script in the file `/usr/local/bin/chkdaemon` and make the file executable:

```
```sh
# chmod 755 /usr/local/bin/chkdaemon
```
```

To use the script, simply pass it the name of a daemon as an argument. For instance, to check whether dhcpd is running and, if it isn’t, restart it, use the command:

```
```sh
# chkdaemon dhcp
```
```

The logic of the script is simple:

+   - On line 6 the path for the script is set. You can only check and restart daemons that exist on the path. Alter the path if you need to use the scripts for daemons that exist in other directories.
+   - On lines 11–14, a check is made to see if the specified daemon exists on the path and, if not, the script exists with an error.
+   - Line 16 determines the PID of the specified daemon using the `pidof` command.
+   - On line 17–21, the script first checks if a PID was found for the daemon. If not, a message is echoed to a log file, the script is started, and an email message is sent to the root user indicating that the daemon was started.

If you have critical system services, you can schedule this script to run on a regular basis as outlined in Chapter 7, “Scheduling Tasks.”

# Source Code

> > **Note**  
> > The line numbers are provided for reference purpose only.

```
```sh
01: #!/bin/sh
02: # Script to check if a daemon is running.
03: # If not start it and notify root
```
```