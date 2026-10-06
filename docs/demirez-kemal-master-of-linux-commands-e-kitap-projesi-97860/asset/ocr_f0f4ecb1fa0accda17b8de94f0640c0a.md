# 252 | Master of Linux Commands

At this stage, we need to make an arrangement in Kali system. If there will be the ssh connection attempt to made to Kali, system will deny the connection and give a **permission denied warning**. If you receive such a warning on the Linux distribution you are using you can do the same arrangements we will do shortly. SSH service configuration file is `/etc/ssh/sshd_config` file. We will make an arrangement on this file. Now let's open the file with any text editor. (I use `nano` editor: `nano /etc/ssh/sshd_config`)

| GNU 2.2.6 File:/etc/ssh/sshd_config |
| HostKey /etc/ssh/ssh_host_rsa_key |
| HostKey /etc/ssh/ssh_host_dsa_key |
| HostKey /etc/ssh/ssh_host_ecdsa_key |
| HostKey /etc/ssh/ssh_host_ed25519_key |
| #Privilege Separation is turned on for security |
| UsePrivilegeSeparation yes

+   * Lifetime and size of ephemeral version 1 server key
KeyRegenerationInterval 3600
ServerKeyBits 1024

```
# Logging
SyslogFacility AUTH
LogLevel INFO

# Authentication:
LoginGraceTime 120
PermitRootLogin without-password
StrictModes yes
```

Let's delete without-password expression where **Authentication** written and write yes statement.

```
# Authentication:
LoginGraceTime 120
PermitRootLogin without-password
StrictModes yes
```