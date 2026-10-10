
## TABLE 11.5 Common rdesktop Options

| Command Name | Effect |
| :--- | :--- |
| -u username | Specify a username for accessing the server. |
| -d domain | Specify a domain for accessing the server. |
| -s shell | Start the specified program rather than Explorer on the server. |
| -p password | Pass the specified password to the server. This may have no effect if the Always Prompt for Password option is set on the server. |
| -g geometry | Specify the desktop size; geometry is specified as width and height, separated by an x, as in 1024x768. |
| -f | Enter full-screen mode. |
| -a bitdepth | Specify the color depth (8, 15, 16, or 24). Depths greater than 8 work only with Windows XP or newer. |

## Using VNC

VNC’s greatest strength is its cross-platform nature. VNC clients and servers are available for Linux, other Unix variants, Mac OS, Windows, and more obscure O/Ss. This makes VNC a good choice for remote GUI access in a cross-platform environment.

### Configuring a VNC Server

The standard VNC server configuration on Linux is rather odd: it runs the VNC server as an ordinary user. Accessing the server produces a login to the computer as the user who ran the server. Thus, if Fred and Mary both run VNC servers on a Linux system, each can log in separately; but if George and Sally also have accounts on the system but don’t run VNC, they won’t be able to log in remotely. Behind the scenes, VNC server programs for Linux include both a VNC server and an X server; the two are linked, with the VNC server half functioning as a virtual keyboard, mouse, and monitor for the X server half.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_536_0.png)

It’s possible to link VNC to an X Display Manager Control Protocol (XDMCP) server. When this is done, users who access the VNC server system will see a standard Linux XDMCP login screen. This configuration requires using advanced VNC options that aren’t described here.

The first step to running VNC is to install it. Several different VNC servers exist, and most distributions ship with at least one of them. Typically, separate client and server packages are available, often called vnc and vnc-server, or variants of this (such as tightvnc and tightvncserver). If you’re not sure whether VNC is installed on your system, use your high-level package manager, such as yum or apt-get, to search for relevant packages. If VNC isn’t installed, install the appropriate packages for your distribution, or check the RealVNC Web site (http://www.realvnc.com/) or the Tight VNC Web site (http://www.tightvnc.com). After you install VNC, follow these steps as an ordinary user on the VNC server system:

- 1. Create a directory called ~/.vnc in your home directory. This directory will house your VNC configuration files.
- 2. Type vncpasswd. The program prompts you for a password and for a verification of this password. VNC doesn’t, by default, use the normal Linux password database. You will need this password to gain entry to the system.
- 3. Type vncserver. This command is actually a script that performs various checks and then starts a VNC server (using the Xvnc program file) in your name. The program displays some summary information, including a VNC session number:

```
New `tranquility.luna.edu:1` (`neil`) `desktop is` `tranquility.luna.edu:1`
```

You should now be able to access this VNC server system, as described in the upcoming section “Using a VNC Client.” When you try this, though, you may run into problems. One common issue is that the server fails to start, or it starts and then crashes. Check for log files in `~/.vnc`. These files may include clues to the problem. One common problem relates to font paths; the VNC server is very sensitive about its font paths, and it will crash if you specify font directories that don’t exist or that are misconfigured. You can add the -fp option and a comma-separated list of font directories to the command line to work around this problem. Alternatively, you can adjust your configuration files.

A second problem—or series of problems, really—is that various default options may be set strangely. Most configurations use two types of configuration files:

**The VNC Startup Script** The `vncserver` script includes within it various options, such as the default desktop size, the default font path, and so on. For the most part, these defaults are equivalent to X server defaults you would set in your local X server’s xorg.conf file. You can edit this script to change these defaults.

**User Configuration Files** Most VNC servers use `~/.vnc/xstartup` as a user’s local startup script. This script may call `/etc/X11/xinit/xinitrc` or some other local default startup script, or it may launch a bare-bones window manager, such as twm. In any event, you can edit this script much as you’d edit any other X startup script.

## Using a VNC Client

The Linux VNC client program is usually called `vncviewer`. This tool takes several options, but in most cases you use it by typing the program name followed by the VNC server name, a colon, and the VNC session number. For instance, you might type the following command:

```
$ vncviewer blueox.luna.edu:1
```

VNC server supports protocol version 3.8 (viewer 3.3)

Password:

If you type the correct password, `vncviewer` displays more text in your terminal and opens a window displaying the remote computer's desktop. VNC clients are also available for many other OS; check the original VNC or the Tight VNC Web sites for these clients. These non-Linux VNC clients work much like the Linux VNC client, but they emphasize dialog boxes for entering the server's hostname and password.

One important drawback of VNC is that the user must ordinarily launch the VNC server from the server computer before running the VNC client program from the client computer. In some cases, this requirement isn't a major issue. For instance, if you're sitting at a workstation and know you'll want to use it from another location in the near future, you can launch the server before leaving the workstation. In other cases, though, you may need to log into the VNC server computer using a text-mode login tool in order to launch the VNC server. This procedure requires two logins, which is a nuisance. What's more, this means you must run two login protocols on the server computer, increasing its security exposure.

## Deploying MySQL

The Structured Query Language (SQL), as its expanded name suggests, is a language used for retrieving data from a database. In practice, SQL is implemented in several different database products. Thus, you should know a little about the SQL products that are available for Linux. With a SQL package installed, you can begin learning about the principles of SQL use and run a SQL product.

### Picking a SQL Package

SQL is a language for accessing data, and specific SQL packages implement that language. This distinction is similar to that between a network protocol (such as SMTP) and the servers that implement it (such as sendmail and Postfix). In principle, you can use any SQL package to satisfy your SQL database needs. In practice, specific products that store data using SQL may work better with (or even require) particular packages. Some of the more common choices in Linux include the following:

**MySQL** Sun owns this SQL implementation, which it has released under the GPL. Most major Linux distributions include MySQL in their package databases. For a complete installation, you'll probably need to install multiple packages, such as a client, a server, and perhaps development tools. You can learn more at [http://www.sun.com/software/products/mysql/](http://www.sun.com/software/products/mysql/).

**PostgreSQL** This SQL implementation evolved from the earlier Ingres software (the name *PostgreSQL* is a compressed form of *post-Ingres SQL*). It’s available under the BSD license and is available as multiple packages in most Linux distributions. As with MySQL, you’ll most likely have to install a client, a server, and perhaps additional support packages. PostgreSQL is headquartered at http://www.postgresql.org.

**SQLite** This package, based at http://www.sqlite.org, is a library that implements SQL. As such, it’s not a stand-alone database; instead, it’s intended as a way to provide programs with access to SQL database features within the program. If you install a program that uses SQLite, your distribution’s package manager should install the relevant libraries for you. If you want to write a program that requires database access and you don’t want to install a complete client-server SQL package such as MySQL or PostgreSQL, SQLite may be just what you need.

There are dozens more SQL database products for Linux. For the purpose of learning SQL, MySQL, or PostgreSQL should do fine, or you can use another full implementation if you prefer. If you have a specific purpose in mind for using SQL, though, you should research SQL packages in more detail. You may need a particular product for compatibility with other software, or you may need a SQL package that provides specific features. The Linux+ objectives mention only MySQL by name.

As just noted, some SQL packages, including MySQL and PostgreSQL, operate on a client-server model: one program (the server) manages the database, while another (the client) provides users and programs with access to the database. Such implementations can work over a network, enabling users at multiple client systems to access a centralized database server.

### Using MySQL

To learn about SQL, you should have access to a SQL database. For purposes of demonstration, I’m using MySQL as a reference. Other SQL implementations are similar to what I describe here, but some details differ. From an administrative perspective, you need to know how to set MySQL configuration options, how to start and stop the server, and how to test that it’s working. Actually performing database queries with MySQL is a complex topic that’s beyond the scope of this book or the Linux+ exam.

#### Configuring, Starting, and Stopping MySQL

MySQL’s main configuration file is called *my.cnf*, and it’s usually stored in /etc/ or /etc/mysql/. You should peruse this file to familiarize yourself with some of the key MySQL options. Unless you know you need to change the defaults, though, you should be cautious about changing this file’s contents, at least initially.

One initial configuration task you must perform is to set the MySQL root password. Just like Linux itself, MySQL requires an administrative (root) user; however, MySQL’s root isn’t the same as the Linux root account. A default MySQL installation is likely to
