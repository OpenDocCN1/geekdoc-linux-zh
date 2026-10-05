
# journalctl - Logging Services and Events

```
dm-event.socket loaded active listening Device-mapper daemon FIFOs
lvm2-llmpold.socket loaded active listening LVM poll daemon socket
...output omitted...
systemd-udev-control.socket loaded active running udev Control Socket
systemd-udev-kernel.socket loaded active running udev Kernel Socket
```

LOAD = Reflects whether the unit definition was properly loaded.
ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
SUB = The low-level unit activation state, values depend on unit type.

12 listed units.
To show all installed files use 'systemctl list-unit-files'.

- 4. Explore the status of the chronyd service. This service is used for network synchronization (NTP).

- 4.1. Display the status of the chronyd service. Note the process ID of any active daemons.

```
[student@server ~]$ systemctl status chronyd
chronyd.service - NTP client/server
Loaded: loaded (/usr/lib/system/system/chronyd.service; enabled; vendor preset preset: enabled)
Active: active (running) since Wed 2019-02-06 12:46:57 IST; 7 min ago
Docs: man-chronyd(8)
-chronyd.conf(5)
Process: 684 ExStartPost=/usr/libexec/chrony-helper update-daemon
(code=exited,status=SUCCESS)
Process: 673 ExStart=/usr/sbin/chronyd $OPTIONS (code=exited,status=0)
```

```
Main PID: 680 (chronyd)
Tasks: 1 (limit: 11406)
Memory: 1.5M
Group: /system.slice/chronyd.service
L-680 /usr/sbin/chronyd
```

```
jequi.lt.example.com.systemd[1]: Starting NTP client/server...
...output omitted...
jequi.lt.example.com.systemd[1]: Started NTP client/server.
servera.lab.example.com chronyd[680]: Source 172.25.254.254 offline
servera.lab.example.com chronyd[680]: Source 172.25.254.254 online
servera.lab.example.com chronyd[680]: Selected source 172.25.254.254
```

- 4.2. Confirm that the listed demons are running. In the above command, the output of the process ID associated with the chronyd service is 680. The process ID might differ on your system.

```
[student@server ~]$ ps -p 680
PID TTY TIME CMD
680 ? 00:00:00 chronyd
```

- 5. Explore the status of the sshd service. This service is used for secure encrypted communication between systems.

- 5.1. Determine whether the sshd service is enabled to start at system boot.

```
[servera ~$]$ systemctl is-enabled sshd
enabled
```

- 5.2. Determine if the sshd service is active without displaying all of the status information.

```
[servera ~$]$ systemctl is-active sshd
active
```

- 5.3. Display the status of the sshd service.

```
[servera ~$]$ systemctl status sshd
* sshd.service - OpenSSH server daemon
   Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; preset: enabled)
   Active: active (running since 2019-02-06 12:46:58 IST; 4h 21min ago)
   Docs: sshd(8)
      sshd.config(5)
   Main PID: 720 (sshd)
   Tasks: 1 (limit: 11406)
   Memory: 5.8M
   CGroup: /system.slice/sshd.service
      /usr/sbin/sshd -D -ciphers=aes256-gcm@openssh.com,sha256-poly1305@openssh.com,aes256-ctr,aes256-bc,aes128-gcm@openssh.com,aes128-ctr,aes128-bc -hmac=hmac-sha256-etm@openssh.com,hmac-sha256-sha
      gequi.init.example.com systemd[1]: Starting OpenSSH server daemon...
      server.la.example.com sshd[720]: Server listening on 0.0.0.0:port 22.
      server.la.example.com systemd[1]: Starting OpenSSH server daemon.
      server.la.example.com sshd[720]: Server listening on ::port 22.
      ...output_merged...
      server.la.example.com sshd[1380]: pam_unix(sshd:session): session opened for
      user by (uid=0)
```

Press Q to exit the command.

- 6. List the enabled or disabled services of all units service.

```
[servera ~$]$ systemctl list-unit-files --type=service
```

| UNIT FILE | STATE |
| :--- | :--- |
| arp-ethers.service | disabled |
| atd.service | enabled |
| audit.service | enabled |
| auth-rcpgss-module.service | static |
| autovt.service | enabled |
| blk-availability.service | disabled |

```
chrony-dnssrv.service    static
chrony-wait.service     disabled
chronyd.service         enabled
...output omitted...
```

Press **Q** to exit the command.

- 7. Exit from servera.

```
[student@servera ~]$ exit
logout
Connection to servera closed.
[student@workstation]$
```

# Finish

On workstation, run the **lab services-identify finish** script to complete this exercise.

```
[student@workstation ~]$ lab services-identify finish
```

This concludes the guided exercise.

# CONTROLLING SYSTEM SERVICES

# OBJECTIVES

After completing this section, you should be able to control system daemons and network services.

# STARTING AND STOPPING SERVICES

Some services require that other services be running first, creating dependencies on the other. Services are not started at boot but rather on demand. In both cases, systemd systemctl starts as needed to resolve the dependency or to start an frequently used service. For example, if the CUPS service is not running and a file is placed into the print directory, the system will start CUPS-related daemons to satisfy the print request.

To start a service, first verify it is not running. Using systemd systemctl start. The example below shows how to start:

```
[root@host ~]$ systemctl start
```

To completely stop printing services on a system, stop all units. Disabling the service disables the dependencies.

To stop a running service, use the stop command. The example below shows how to stop:

```
[root@host ~]$ systemctl stop
Warning: Stopping cups, but it can still be activated by:
cups.path
cups.socket
```

# RESTARTING AND RELADING SERVICES

Some services have the ability to reload their configuration without requiring a restart. This process is called a reload. Reloading a service does not change the process ID. To restart a service, use the restart command. The example below shows how to restart:

```
[root@host ~]$ systemctl restart
```

# CONTROLLING SERVICES

CHAPTER 7 | Controlling Services and Dependencies

In you are not sure whether the service has the functionality to reload the configuration, use the reload-restart argument with the command. The command reloads the configuration if reloading functionality is available. Otherwise, the command restarts the service to:

```
[root@host ~]$ systemctl reload-restart
```

# LISTING UNIT DEPENDENCIES

The systemctl list-dependencies UNIT displays a hierarchy mapping of dependencies to start the service unit. To reverse dependencies (units that depend on the specified unit), use the --reverse option with the command.

```
[root@host ~]$ systemctl list-dependencies sshd.service
sshd.service
• --system.slice
• --ssh-keygen.target
• --ssh-keygen@ecdsa.service
• --ssh-keygen@ed25519.service
• --ssh-keygen@rsa.service
• --sysinit.target
• --output omitted..
```

# MASKING AND UNMASKING SERVICES

At times, a system may have different services installed that are conflicting with each other. For example, there are multiple methods to manage mail servers (postfix and sendmail, for example). Masking a service prevents an administrator from accidentally starting a service that conflicts with others. Masking creates a link in the configuration directories to the /dev/null file which prevents the service from starting.

```
[root@host ~]$ systemctl mask sendmail.service
Created symlink /etc/systemd/sendmail.service -> /dev/null.
```
