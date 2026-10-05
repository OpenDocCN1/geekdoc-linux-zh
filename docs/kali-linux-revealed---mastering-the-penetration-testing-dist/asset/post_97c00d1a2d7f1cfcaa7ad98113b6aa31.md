
Alternatively, you can also force the expiration of a password using the passwd -e user command, which forces the user to change their password the next time they log in.

## 5.2.3. Disabling an Account

You may find yourself needing to disable an account (lock out user) as a disciplinary measure, for the purposes of an investigation, or simply in the event of a prolonged or definitive absence of a user. A disabled account means the user cannot login or gain access to the machine. The account remains intact on the machine and no files or data are deleted; it is simply inaccessible. This is accomplished by using the command passwd -l user (lock). Re-enabling the account is done in similar fashion, with the -u option (unlock).

## 5.2.4. Managing Unix Groups

The add and delroup commands add or delete a group, respectively. The groupmod command modifies a group's information (its gid or identifier). The command gpasswdwd changes the password for the group, while the gpasswd -r group command deletes it.

| Working with Several Groups | Each user may be a member of many groups. A user's main group is, by default, created during initial user configuration. By default, each file that a user belongs to the user, as well as to the user's main group is not always desirable; for example, when the user needs to work in a directory shared by other group. In this case, the user needs to change groups using one of the following commands: newgrp, which starts a new shell, or sg, which executes a command using the specified group. These commands also allow you to join a group to which they do not belong. If the group is protected, they will need to supply the appropriate password before the command is executed. Alternatively, the user can set the setgid bit on the directory, which causes files created in that to automatically belong to the correct group. For more details, see setgid directory and sticky bit [page 58]. The id command displays the current state of a user, with their personal identifier (uid variable), current main group (gid variable), and the list of groups to which they belong (groups variable). |

## 5.3. Configuring Services

In this section we will take a look at services (sometimes called daemons), or programs that run as a background process and perform various functions for the system. We will start by discussing configuration files and will proceed to explain some important services (such as SSH, PostgreSQL, and Apache) function and how they can be configured.

## 5.3.1. Configuring a Specific Program

When you want to configure an unknown package, you must proceed in stages. First, you should read the package maintainer has documented. The /usr/share/doc/package/README.Debian is a good place to start. This file will often contain information about the package, including pointers that may refer you to other documentation. If you save yourself a lot of time, and avoid a lot of frustration, by reading this file first it details the most common errors and solutions to most common problems.

Next, you should look at the software’s official documentation. 6.1, "Documentation Sources" [page 124] for tips on how to find various documentation sources. The dpkg-package gives a list of files included in the package; you can quickly identify the available documentation (as well as the configuration files, located in /etc/). Also, dpkg -s package displays the package meta-data and shows any recommended or suggested packages; in others, you can find documentation or use a utility that will help the configuration of the software.

Finally, the configuration files are often self-documented by explanatory comments detailing the various values for each configuration setting. In some cases, you can get up and running byにつき a single line in the configuration file. In other cases of configuration files are provided in the /usr/share/doc/package/examples/ directory. They may serve as a base for your own configuration file.

## 5.3.2. Configuring SSH for Remote Logins

SSH allows you to remotely log into a machine, transfer files, or execute commands. It is an standard tool (ssh) and service (sshd) for connecting to remotely machines.

While the openssh-server package is installed by default, the SSH service is disabled by default and is not started at boot time. You can manually start the SSH service with systemctl start or configure it to start at boot with systemctl enable ssh.

The SSH service has a relatively default config, but given its powerful capabilities and sensitive nature, it is good to know what you can do with its configuration file, /etc/ssh/sshd_config. All the options are documented in sshd_config(5).

The default configuration disables password-based logins for the root user, which means you must first set up SSH keys with ssh-keygen. You can extend this to all users by setting PasswordAuthentication to no, or you can lift this restriction by changing PermitRootLogin yes (instead of the default prohibit-password). The SSH service listens by default on port 22 you can change this with the Port directive.

To apply the new settings, you should run systemctl reload ssh.

## Generating New SSH Keys

Each SSH server has its own cryptographic keys; they are named "SSH host keys" and are stored in /etc/ssh/ssh_host_*. They must be kept private if you want confidentiality and they should not be shared by multiple machines.

When you install your system by copying a full disk image (instead of debian-installer), the image might contain pre-generated SSH host keys that you should replace with newly-generated keys. The image probably comes with a default root password that you want to reset at the same time. You can do all with the following commands:

```
# password
# rm /etc/ssh/ssh_host_*
# dpkg-reconfigure openssh-server
# service restart
```

## 5.3.3. Configuring PostgreSQL Databases

PostgreSQL is a database server. It allows for multiple versions of clusters.

| Multiple PostgreSQL versions | The postgresql.conf can be configured with various directives: listen_addresses for the addresses to listen to, port for the TCP port, and unix_socket_directories to define the directory where the file-based sockets are created var/run/postgresql/. |

## Connection Type and Authentication

Depending on how they connect, clients are authenticated in different ways. The pg_hba.conf configuration file defines who is allowed to connect on each socket and how they are authenticated. By default, connections on the file-based socket use the Unix account as the name of the PostgreSQL, and it assumes that no further authentication is required. The TCP connection requires the user to authenticate with a username and password (though not a Unix username/password rather than one by PostgreSQL).

The postgres user is special and has full administrative privileges over all databases. We will use this identity to create new users and new databases.

## Creating Users and Databases

The createuser command adds a new user and dropdb removes one. Likewise, the createdb command adds a new database and removes one. Each of these commands have their own pages but we will discuss some of the options here. Each command on the default cluster (running on 5432) you can use --port to modify acts and databases of an alternate cluster.

These commands must connect to the PostgreSQL server to do their job and must be authenticated as a user with sufficient privileges to execute the specific operation. The easiest way to achieve this is to use the postgres Unix account and connect over the file-based socket:

```
# su - postgres
$ createuser -P king_phisher
Enter password for new role:
Enter it again:
$ createdb -T template0 -E UTF-8 -O king_phisher king_phisher
```

In the example above, the -P option asks to query for a password once it creates the new king_phisher user. Looking at the createdb command, the -O defines the user owning the new database (which will have full rights to create tables and grant permissions and so on). We also want to be Unicode strings, so we add the -E UTF-8 option to set the encoding, which in turn requires us to use the -T to pick another database template.
