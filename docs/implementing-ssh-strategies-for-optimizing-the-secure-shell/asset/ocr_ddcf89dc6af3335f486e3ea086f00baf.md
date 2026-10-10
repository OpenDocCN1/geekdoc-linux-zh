# **Table 2.15** Options in the SSH1 Compatibility Section (Unix)

| OPTION | DESCRIPTION |
| --- | --- |
| Ssh1Compatibility | Enables (yes) or disables (no) compatibility with SSH version 1, which is an entirely different implementation of SSH when compared with SSH version 2. SSH version 1 is insecure, but may be required. |
| Sshd1Path | Identifies the location of the SSH version 1 binary (for example, /usr/local/sbin/sshd1). |
| Sshd1ConfigFile | Identifies the location of the SSH version 1 configuration file (for example, /etc/ssh1/sshd1_config). |

# Chrooted Environment

The Chrooted Environment allows specific users to be limited to their home directories, either with a shell or with file transfer. In addition to entering the correct information in the sshd2_config file, the ssh-chroot manager needs to be initiated. The Chrooted Environment section of the sshd2_config file should look like the following:

```
# ChRootUsers ftp, guest
# ChRootGroups guest
```

Table 2.16 describes the Chroot options available for the SSH server.

# **Table 2.16** Options in the Chrooted Environment Section (Unix)

| OPTION | DESCRIPTION |
| --- | --- |
| ChRootUsers | Identifies the users that should be limited to their home directories, thus chroot users |
| ChRootGroups | Identifies the groups that should be limited to their home directories, thus chroot groups |

# Subsystem Definitions

The Subsystem Definitions section of the sshd2_config file should look like the following:

```
subsystem-sftp sftp-server
```