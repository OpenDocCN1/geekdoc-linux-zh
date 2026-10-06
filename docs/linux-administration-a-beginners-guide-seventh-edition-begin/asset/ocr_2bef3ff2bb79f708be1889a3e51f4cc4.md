# 592 Linux Administration: A Beginner's Guide

On a Debian-based distro such as Ubuntu, you can use startup's daemon control commands—status, start, reload, and stop—to control the OpenSSH daemon.

For example, view the current status of the OpenSSH daemon on an Ubuntu distro that is not yet systemd enabled, type

```
master@ubuntu-server:-$ sudo status ssh
```

To start the OpenSSH server, you would run

```
master@ubuntu-server:-$ sudo start ssh
```

To stop the daemon, run this:

```
master@ubuntu-server:-$ sudo stop ssh
```

> NOTE Debian-based distros such as Ubuntu refer to the scripts that control the OpenSSH server as ssh. Red-Hat distros refer to the equivalent distros as sshd.

> TIP On an openSUSE, the command to check the status of sshd is opensuse-server:- # rcsshd status And to start it, the command is opensuse-server:~ # rcsshd status

# SSHD Configuration File

Out of the box, Linux systems already have the OpenSSH server configured and running with various default settings.

On most RPM-based Linux distributions, such as Fedora, Red Hat Linux (RHEL), openSUSE, CentOS, the main configuration file for sshd_config usually resides under the /etc/ssh/ Debian-based distros also store the configuration files under /etc/ssh/. For the OpenSSH version that was installed from source, the configuration file is located under /usr/local/etc/etc.

Next'll discuss some of the configuration options found in the sshd_config file:

+   * AuthorizedKeys Specifies the path to the file that contains the public keys that can be used for user authentication. The default is /<User_Home_Directory>/.authorized_keys.

+   * Ciphers This is a comma-separated list of ciphers allowed for the SSH protocol version 2. Examples of supported are 3des-cbc, aes256-cbc, aes256-ctr, and blowfish-cbc.

+   * HostKey defines the file containing a private key used by SSH. The default is either /etc/ssh/ssh_host_rsa_key or /etc/ssh/ssh_host_dsa_key or /etc/ssh/ssh_host_ecdsa_key, or /etc/ssh/ssh_host_ed25519 for protocol version 2.