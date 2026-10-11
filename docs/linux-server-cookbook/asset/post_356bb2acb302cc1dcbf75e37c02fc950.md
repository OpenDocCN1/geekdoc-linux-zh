
(Reading database ... 100820 files and directories currently installed.)
Removing ssl-cert (1.1.2) ...
Processing triggers for man-db (2.10.2-1) ...

![](img/863afa537de4eed7deb11978bfbfa90e_139_0.png)

The command **apt-cache** is used to query the local index of packages retrieved from the software repositories. The common actions are shown in table 4.24:

| Action | Description |
| :----- | :---------- |
| show | Show information about one specific package. |
| search | Search in the index for the specific pattern. |
| depends | Lists the dependencies needed for the specified package. |

Table 4.24: Actions for the command apt-cache

The following figures and examples of the common uses for **apt-cache** are provided:

- Get information about the package **firefox**, as shown in figure 4.51:

```
root@ubuntu:~# apt-cache show firefox
Package: firefox
Architecture: amd64
Version: 1:1snap1-0ubuntu2
Priority: optional
Section: web
Origin: Ubuntu
Maintainer: Ubuntu Mozilla Team <ubuntu-mozillateam@lists.ubuntu.com>
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Installed-Size: 255
Provides: gnome-www-browser, iceweasel, www-browser, x-www-browser
Pre-Depends: debconf (>= 0.5) | debconf-2.0
Depends: firefox-dbgsym (<< 1:1snap1), firefox-dev (<< 1:1snap1), firefox-geckodriver (<< 1:1snap1), firefox-mozsymbols (<< 1:1snap1)
Replaces: firefox-dbgsym (<< 1:1snap1), firefox-dev (<< 1:1snap1), firefox-geckodriver (<< 1:1snap1), firefox-mozsymbols (<< 1:1snap1)
Filename: pool/main/f/firefox/firefox_1snap1-0ubuntu2_amd64.deb
Size: 72292
MD5sum: 4cfb8522595425213edbd344d0dfa6b6
SHA1: ec27ebdf84c2d918ad669cfc94f1163b5937c4dfb66
SHA256: d6ccd2ef5cc7291364ab49bb9e57d68a4ac993488ae561bb67ed31dd6b17659cc
SHA512: 35cb18af4766668b7735713277786946fe2f90abba2f5cabd55f73124de672645a07ac9a6e12ca66677d892f07356f3a90d8c521b5b657b394949b146601f2a
Description-en: Transitional package - firefox -> firefox snap
This is a transitional dummy package. It can safely be removed.
.
firefox is now replaced by the firefox snap.
Description-md5: 28593f0124b124447f7e30b88c6717ba4
Translators:
The Ubuntu l10n Team <ubuntu-devel@lists.
```

![](img/863afa537de4eed7deb11978bfbfa90e_140_0.png)

- Search for packages with pattern `^ansible` (name or description starts with word ansible), as shown in figure 4.52:

```
root@ubuntu:~# apt-cache search ^ansible
ansible - Configuration management, deployment, and task execution system
ansible-core - Configuration management, deployment, and task execution system
ansible-lint - lint tool for Ansible playbooks
ansible-mitogen - Fast connection strategy for Ansible
shade-inventory - Ansible inventory script for OpenStack clouds
```

![](img/863afa537de4eed7deb11978bfbfa90e_140_1.png)

- Show the dependencies for the package python3-urllib3, as shown in figure 4.53:

```
root@ubuntu:~# apt-cache depends python3-urllib3
python3-urllib3
  Depends: <python3:any>
    python3
  Depends: python3-six
  Recommends: ca-certificates
  Suggests: python3-cryptography
  Suggests: python3-idna
  Suggests: python3-openssl
  Suggests: python3-socks
```

![](img/863afa537de4eed7deb11978bfbfa90e_141_0.png)

The command `apt` is a frontend for the commands `apt-get` and `apt-cache`. The actions available for the command are shown in table 4.25:

| Action | Equivalent | Action | Equivalent |
| :--- | :--- | :--- | :--- |
| update | `apt-get update` | reinstall | `apt-get install` |
| upgrade | `apt-get upgrade` | remove | `apt-get remove` |
| full-upgrade | `apt-get dist-upgrade` | purge | `apt-get purge` |
| install | `apt-get install` | autoremove | `apt-get autoremove` |
| search | `apt-cache search` | show | `apt-cache show` |

![](img/863afa537de4eed7deb11978bfbfa90e_141_1.png)

## Introduction to services

A Linux service (or sometimes called **daemon**) is an application or set of applications that are running in the background performing some tasks or waiting for some event. Some services can execute some applications, and when it finishes, the service is stopped. An example is a service to configure the network in the system. Other services are running constantly, waiting to offer some resource; for example, an **SSH** service is waiting for users to connect and offer the possibility to login to the server.

Most Linux distributions use the service manager called **systemd**, which is a replacement for the historical and popular **SysV init** daemon. When a Linux distribution is booted, the first process executed is **systemd**, and it will be responsible for starting the rest of the services enabled in the system to be started on boot.

**Systemd** is a full suite of applications aiming to unify the service configuration and the behavior across different *Linux distributions*. The main command to manage services is `systemctl`, and the popular actions are described in table 4.26:

| Action | Description |
| :--- | :--- |
| list-units | List the *units* (services, mount points, devices, and sockets) available in the system. |
| status | Check the status of the specified *unit(s).* |
| show | Show the properties of the specified *unit(s).* |
| start | Start the *unit(s)* specified. |
| stop | Stop the *unit(s)* specified. |
| reload | The *unit(s)* specified will reload the configuration. |
| restart | Stop and start the *unit(s)* specified. |
| enable | Enable the *unit(s)* specified to be started when the system boots. |
| disable | Disable the *unit(s)* specified to do not be started when the system boots. |

Table 4.26: Actions for systemctl

In the following figures, some examples of the actions for the command `systemctl` listed are shown:

- Check the status of the service named `cron`, as shown in figure 4.54:

![](img/863afa537de4eed7deb11978bfbfa90e_142_0.png)

Figure 4.54: Output example about the status of one service.

- Disable a service what is currently enabled, as shown in figure 4.55:

![](img/863afa537de4eed7deb11978bfbfa90e_142_1.png)

Figure 4.55: Output example disabling a service.

- Enable a disabled service, as illustrated in figure 4.56:

```
root@ubuntu:~# systemctl enable cron
Synchronizing state of cron.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable cron
Created symlink /etc/systemd/system/multi-user.target.wants/cron.service → /lib/systemd/system/cron.service.
```

> Figure 4.56: Output example enabling a service.

### Conclusion

Administrating users and groups is one of the main tasks for Linux administrators and regular users administrating a system. Linux provides easy-to-use tools to perform all the user and group-related tasks, such as create, query, modify, or delete.

Other important knowledge needed when working with a Linux distribution is to know how to install and administrate software in the system. Understanding the package format and software repositories and the tools available are needed skills to configure a system, install new software and then install new services on it. Services are applications usually running in the background, performing some tasks or offering some service to regular users.

### Key facts

- Users and groups information are stored in plain files.
- Passwords are encrypted and saved in files only accessible by administrators.
- Linux Distributions provide several tools to operate with users and groups.
- Package Format for distributions helps in the installation process of new software and updates the system.
- Software repositories keep software and libraries to be accessible from the system and the system tools to install the software.
- Services are processes running in the background performing some operating or waiting to offer functionality.

### Questions

1. What option for command useradd is creating the directory for the user?
   a. -h, --create-home
   b. -m, --create-home
   c. -d, --create-directory
2. Which of the following commands are not used to operate with RPM packages?
