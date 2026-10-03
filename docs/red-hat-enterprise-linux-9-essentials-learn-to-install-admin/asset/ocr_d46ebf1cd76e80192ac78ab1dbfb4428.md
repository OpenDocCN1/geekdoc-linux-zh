# Configuring SSH Key-based Authentication on RHEL 9

```
[neil@demosystem02 ~]$
```

Repeat these steps for any other accounts on the server for which remote access is required. If access is also required from other client systems, copy the id_rsa private key file to the .ssh subdirectory of your home folder on the other systems.

As currently configured, access to the remote system can still be achieved using less secure password authentication. Once you have verified that key-based authentication works, password authentication will need to be disabled on the system. To understand how to change this setting, begin by opening the /etc/ssh/sshd_config file and locating the following line:

```
Include /etc/ssh/sshd_config.d/*.conf
```

This tells us that sshd configuration settings are controlled by files in the /etc/ssh/sshd_config.d directory. These filenames must be prefixed with a number and have a .conf filename extension, for example:

```
01-permitrootlogin.conf
50-redhat.conf
```

The number prefix designates the priority assigned to the file relative to the other files in the folder, with 01 being the highest priority. This ensures that if a configuration file contains a setting conflicting with another file, the one with the highest priority will always take precedence.

Within the /etc/ssh/sshd_config.d folder, create a new file named 02-nopasswordlogin.conf with content that reads as follows:

```
PasswordAuthentication no
```

Save the file and restart the sshd service to implement the change:

```
# systemctl restart sshd.service
```

From this point on, it will only be possible to remotely access the system using SSH key-based authentication, and when doing so, you won’t be required to enter a password.

# 15.6 Managing Multiple Keys

It is common for multiple private keys to reside on a client system, each providing access to a different server. As a result, several options exist for selecting a specific key when establishing a connection. It is possible, for example, to specify the private key file to be used when launching the ssh client as follows:

```
$ ssh -l neilsmyth -i ~/.ssh/id_work 35.194.18.119
```

Alternatively, the SSH client user configuration file may associate key files with servers. The configuration file is named config, must reside in the .ssh directory of the user’s home directory, and can be used to configure a wide range of options, including the private key file, the default port to use when connecting, the default user name, and an abbreviated nickname via which to reference the server. The following example config file defines different key files for two servers and allows them to be referenced by the nicknames home and work. In the case of the work system, the file also specifies the user name to be used when authenticating: