# MANAGING NETWORKING

### PERFORMANCE CHECKLIST
In this lab, you will configure networking settings on a Red Hat Enterprise Linux server.

### OUTCOMES
You should be able to configure three static IPv4 addresses for the primary network interface.

### BEFORE YOU BEGIN
Log in as the student user on workstation student as the password.

From workstation run the **lab net-review start** command. The command runs a start script that determines if the host, server, is reachable on the network.

```bash
[student@workstation ~]$ lab net-review start
```

+   1. Use the `ssh` command to log in to server as the `student` user. The systems are configured to use SSH keys for authentication, so a password is not required to log in to server.
2. Use the `sudo -i` command to switch to the `root` user. If prompted, use `student` as the password.
3. Create a new connection with a static network connection using the settings in the table.
4. Configure the new connection to be autostarted. Other connections should not start automatically.
5. Modify the new connection so that it also uses the address 10.0.1/24.
6. Configure the `hosts` file so that 10.0.1.1 can be referenced as `private`.
7. Reboot the system.

| PARAMETER | SETTING |
|---|---|
| Connection name | lab |
| Interface name | ens3 (might vary, use the interface that has 52:54:00:00:fa:0b as its MAC address) |
| IP address | 172.25.250.11/24 |
| Gateway address | 172.25.250.254 |
| DNS address | 172.25.250.254 |