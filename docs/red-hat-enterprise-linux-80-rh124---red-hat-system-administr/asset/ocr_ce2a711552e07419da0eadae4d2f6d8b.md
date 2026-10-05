# Analyzing and Tuning Logs

```
Storage=persistent
...output omitted..
```

3.2. Use the systemctl command to restart systemd-journal service to bring the configuration changes into effect.

```
[student@server ~]$ sudo systemctl restart systemd-journal.service
```

+   4. Confirm the systemd-journal service on server preserves its journals until the journals persist across reboots.

+   4.1. Use the reboot command to restart server.

```
[student@server ~]$ sudo reboot
Connection to server closed by remote host.
Connection to server closed.
[student@workstation ~]$
```

Notice that the SSH connection was terminated as soon as you restarted the server system.

+   4.2. Open an SSH session to server again.

```
[student@workstation ~]$ ssh student@server
...output omitted..
[student@server ~]$
```

+   4.3. Use the ls command to confirm that the /var/log/journal directory exists. The /var/log/journal directory contains a subdirectory that contains a long string of hexadecimal characters as its name. Inside this directory, you will find the journals. You may encounter a directory with different name than the one shown in the following output.

```
[student@server ~]$ sudo ls /var/log/journal
[sudo] password for student: student
73ab164e27e48be9bf80e714a8cd5
[student@server ~]$ sudo ls /var/log/journal/73ab164e27e48be9bf80e714a8cd5
system.journal-user-1000
```

+   4.4. Log out of server.

```
[student@server ~]$ exit
logout
Connection to server closed.
```

# Finish

On workstation, run lab log-preserve finish to complete this exercise. This script ensures the environment is restored to the clean state.