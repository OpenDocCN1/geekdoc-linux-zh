Linux. OpenSSH version 2 no longer makes use of the once-patented RSA public-key algorithm for authentication and fixes a cyclic redundancy check (CRC) problem that compromised the integrity checks in version 1 of the standard.

> **WARNING**  There have been several vulnerabilities found in many of the older SSH v.1 implementations. I suggest that you only use SSH v.2 software.

Let’s take a look at how to install and configure OpenSSH on your Linux server and on other Linux clients.

# Obtaining OpenSSH

The OpenSSH RPM package should be readily available from your favorite Web repository, such as www.rpmfind.net. Look for the following three packages:

+   - `openssh-2.5.2p2-1.7.2-i386.rpm` contains
+       - The man pages
+       - The configuration files
+       - The critical generation utilities
+   - `openssh-server-2.5.2p2-1.7.2-i386.rpm` contains
+       - The sshd daemon
+       - The startup files
+       - The sftp server
+   - `openssh-clients-2.5.2p2-1.7.2-i386.rpm` contains
+       - The ssh client
+       - The sftp client

Once you've obtained these three packages, go ahead and install them (or upgrade them, depending on your situation) with the following commands:

```
[ramon]$ sudo rpm -i openssh-2.5.2p2-1.7.2-i386.rpm
[ramon]$ sudo rpm -i openssh-server-2.5.2p2-1.7.2-i386.rpm
[ramon]$ sudo rpm -i openssh-clients-2.5.2p2-1.7.2-i386.rpm
```

# Configuring OpenSSH

The main OpenSSH daemon configuration file is located in `/etc/ssh/sshd_config`. Entries in this file are of the form:
*variable*   *value*