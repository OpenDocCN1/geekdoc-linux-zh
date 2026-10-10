# Subsystem Definitions

The Subsystem Definitions section of the sshd2_config file should look like the following:

```
```
subsystem-sftp sftp-server2.exe
SftpLogCategory 16
Sftp-DirList "HOME=$D"
Sftp-Home $D
Sftp-AdminDirList "HOME=$D, C:=C:, D:=D:"
# Sftp-AdminUsers
```
```

The SFTP Server section of the SSH configuration GUI should look like Figure 2.12.

The SFTP Server- Power Users section should look like Figure 2.13.

![](bbox=[0.17, 0.38, 0.87, 0.82])

# Figure 2.12

SFTP Server screen from the SSH server configuration tool.