
## User Configuration: .my.cnf

Users who access the database server will have their own configuration file in their home directory: **.my.cnf**. Here the user can specify connection options such as the password used to access the database and the connection timeouts.

```plaintext
[client]
password=mypassword

[mysql]
no-auto-rehash
set-variable = connect_timeout=2

[mysql-hotcopy]
interactive-timeout
```

## Starting and Stopping the MySQL Server

The MySQL server, **mysqld**, can be managed with the `service` command or the `services` tool.

```bash
service mysqld start
```

The **mysqld** script invokes **safe_mysqld**, which is designed to run MySQL on Unix systems, making sure that data directories are set and log files are running. The **safe_mysqld** script in turn will start up the **mysqld** daemon.

## MySQL Tools

MySQL provides a variety of tools (as shown in Table 26-8), including server, client, and administrative tools. Backups can be handled with the **mysqldump** command. The **mysqlshow** command will display a database, just as issuing the SQL command `SELECT *.*` does, and **mysqlimport** can import text files, just like `LOAD INFILE`.

## MySQL Management with mysql and mysqladmin

To manage your MySQL database, you use **mysql** as the **root** user. The **mysql** client starts up the MySQL monitor. As the **root** user, you can enter administrative commands to create databases and database tables, add or remove entries, as well as carry out standard client tasks such as displaying data.

**TABLE 26-8** MySQL Commands

| Command | Description |
| :--- | :--- |
| **mysqld** | MySQL server |
| **mysql** | MySQL client |
| **mysqladmin** | Create and administer databases |
| **mysqldump** | Database backup |
| **mysqlimport** | Import text files |
| **mysqlshow** | Display databases |

Log in as the root user and open a terminal window. Then enter the `mysql` command. This will start a MySQL monitor shell with a `mysql>` prompt. Be sure to end your commands with a semicolon; otherwise, the monitor will provide an indented arrow prompt waiting for added arguments. In the monitor, the semicolon, not the ENTER key, ends commands.

```bash
# mysql -u root -p
mysql>
```

If you have set up a MySQL root user, you can use the `-u root` with the `-p` option. You will be prompted for a password.

```bash
# mysql -u root -p
```

Once the `mysql` client has started, you can use the `status` command to check the status of your server, and `show databases` to list current databases.

```bash
mysql> status;
mysql> show databases;
```

Initially two databases set up by MySQL for its own management are displayed: `mysql` and `test`. The `mysql` database holds MySQL user information, and the `test` database is used to test the server.

## PostgreSQL

PostgreSQL is based on the POSTGRES database management system, though it uses SQL as its query language. POSTGRES is a next-generation research prototype developed at the University of California, Berkeley. You can find more information on it from the PostgreSQL Web site at [www.postgresql.org](http://www.postgresql.org). PostgreSQL is an open source project, developed under the GPL license.

PostgreSQL is often used to provide database support for Internet servers with heavy demands, such as Web servers. With a few simple commands, you can create relational database tables. Use the `createuser` command to create a PostgreSQL user that you can then log in to the server with. You can then create a database with the `createdb` command and construct relational tables using the `create table` directive. With an `insert` command, you can add records and then view them with the `select` command. Access to the server by remote users is controlled by entries in the `pg_hba.conf` file located in PostgreSQL directory, usually `/var/lib/pgsql`.

The Red Hat Linux edition of PostgreSQL also includes the Red Hat Database Graphical tools used to easily manage and access PostgreSQL databases. With the administrator tool, you can browse and manage databases, the Visual Explain tool analyzes query processes, and the Control Center lets you manage databases on servers.

## PART VI

# System Administration

- **CHAPTER 27** Basic System Administration
- **CHAPTER 28** Managing Users
- **CHAPTER 29** Software Management
- **CHAPTER 30** File System Management
- **CHAPTER 31** RAID and LVM
- **CHAPTER 32** Devices and Modules: udev, HAL, and MAKEDEV
- **CHAPTER 33** Kernel Administration: Virtualization
- **CHAPTER 34** Backup Management: rsync, Amanda, and dump/restore

## 27

# Basic System Administration

Linux is designed to serve many users at the same time, providing an interface between the users and the system with its resources, services, and devices. Users have their own shells through which they interact with the operating system, but you may need to configure the operating system itself in different ways. You may need to add new users, devices like printers and scanners, and even file systems. Such operations come under the heading of system administration. The person who performs such actions is referred to as either a *system administrator* or a *superuser*. In this sense, there are two types of interaction with Linux: regular users' interactions, and those of the superuser, who performs system administration tasks. The chapters in this book cover operations such as changing system runlevels, managing users, configuring printers, adding file systems, and compiling the kernel. You perform most of these tasks only rarely, such as adding a new printer or mounting a file system. Other tasks, such as adding or removing users, you perform on a regular basis. Basic system administration covers topics such as system access by superusers, selecting the runlevel to start, system configuration files, and performance monitoring.

With Linux, you have the ability to load different versions of the Linux kernel as well as other operating systems that you have installed on your system. The task of selecting and starting up an operating system or kernel is managed by a boot management utility, the Grand Unified Bootloader (GRUB). This is a versatile tool, letting you load operating systems that share the same disk drive, as well as letting you choose from different Linux kernels that may be installed on the same Linux system.

### Superuser Control: the Root User

To perform system administration operations, you must first have access rights such as the correct password that enables you to log in as the root user, making you the superuser. Because a superuser has the power to change almost anything on the system, such a password is usually a carefully guarded secret, changed very frequently, and given only to those whose job it is to manage the system. With the correct password, you can log in to the system as a system administrator and configure the system in different ways. You can start up and shut down the system, as well as change to a different operating mode, such as a single-user mode. You can also add or remove users, add or remove whole file systems, back up and restore files, and even designate the system's name and address.

*NOTE* If SELinux is enabled, superuser access will be controlled by SELinux rules. See Chapter 17.

To become a superuser, you log in to the *root user account*. This is a special account reserved for system management operations with unrestricted access to all components of your Linux operating system. You can log in as the root user from either the GUI (graphical user interface) login screen or the command line login prompt. You then have access to all administrative tools. Using a GUI interface like GNOME, the root user has access to a number of Red Hat and Fedora GUI administrative tool such as system-config-users for managing users. If you log in from the command line interface, you can run corresponding administrative commands like `rpm` to install packages or `useradd` to add a new user. From your GUI desktop, you can also run command line administrative tools using a terminal window. The command line interface for the root user uses a special prompt, the sharp sign, #. In the next example, the user logs in to the system as the root user and receives the # prompt.

```text
login: root
password:
#
```

### Root User Password

As the root user, you can use the `passwd` command to change the password for the root login, as well as for any other user on the system. The `passwd` command will check your password with Pluggable Authentication Modules (PAM), as discussed in Chapter 28, to see if you’ve selected one that can be easily cracked. To more easily change your root password from a GUI interface, you can use the system-config-rootpassword tool.

```bash
# passwd root
New password:
Re-enter new password:
#
```

You must take precautions to protect your root password. Anyone who gains access as the root user will have complete control over your system. The online manual for the `passwd` command provides detailed recommendations for handling and choosing your password. For example, never store your password in a file on your system, and never choose one based on any accessible information, such as your phone number or date of birth. A basic guideline is to make your password as complex as possible, using a phrase of several words with numbers and upper- and lowercase letters, yet something you can still remember easily so that you never have to write it down. You can access the `passwd` online manual page with the command

```bash
# man passwd
```

### Root User Access: su

While you are logged in to a regular user account, it may be necessary for you to log in as the root and become a superuser. Ordinarily, you would have to log out of your user account first, and then log in to the root. Instead, you can use the `su` command (switch user) to log in directly to the root while remaining logged in to your user account. If you are using a GUI desktop like GNOME, you can enter the `su` command from a terminal window, or use
