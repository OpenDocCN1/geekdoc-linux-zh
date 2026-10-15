
can enter your buddy list as well as set permissions and edit your user information. If a buddy is also logged in, you can click his or her entry and open an instant messenger window to send and receive messages. You can find out more about Kit at kitclient.sourceforge.net. Other AIM clients also available are Kaim and Gaim.

Several GNOME instant messaging clients are designed to work with all instant messaging systems, including AIM, Yahoo, MSN, and ICQ. Gaim has plug-ins that let you connect to ICQ, Yahoo, MSN, IRC, Jabber, and Zephyr. Gabber, a Jabber client, is an open source instant messaging system that allows communication with all other systems, including AIM, Yahoo, MSN, and ICQ. Everybuddy is designed to be a universal instant messenger service for all the major services.

> NOTE Talk is the original Unix talk utility designed to set up an interactive two-way communication between you and another user using a command line interface. It works much like instant messenger. Due to security concerns, you should use talk only on a locally secure system. A K Desktop version of Talk called KTalk displays user screens as panes in a K Desktop window. GNU Talk is a GNOME version of Talk that supports multiple clients, file transfers, encryption, shared applications, auto-answer, and call forwarding.

## Telnet

You use the telnet command to log in remotely to another system on your network. The system can be on your local area network or available through an Internet connection. Telnet operates as if you were logging into another system from a remote terminal. You will be asked for a login name and, in some cases, a password. In effect, you are logging into another account on another system. In fact, if you have an account on another system, you could use Telnet to log into it.

The original version of Telnet is noted for being very insecure. For secure connections over a network or the Internet, you should use the SSH or Kerberos versions of Telnet (see Chapter 18). They operate in the same way as the original but use authentication and encryption to secure the Telnet connection. Even so, it is advisable never to use Telnet to login to your root account.

You invoke the Telnet utility with the keyword telnet. If you know the name of the site you want to connect with, you can enter telnet and the name of the site on the Linux command line. As an alternative, you can use the K Desktop KTelnet utility. This provides a GUI interface to connecting and logging into remote systems.

```
$ telnet garnet.berkeley.edu
Connected to garnet
login:
```

The Telnet program also has a command mode with a series of commands you can use to configure your connection. You can enter the telnet command mode either by invoking Telnet with the keyword telnet or by pressing CTRL-] during a session. The Telnet help command lists all the Telnet commands you can use. A comprehensive list is available on the Man pages (man telnet). In the next example, the user first invokes the Telnet utility. A prompt is displayed next, indicating the command mode, telnet>. The Telnet command open then connects to another system.

```
$ telnet
telnet> open garnet.berkeley.edu
Connected to garnet.berkeley.edu
login:
```

Once connected, you follow the login procedure for that system. If you are logging into a regular system, you must provide a login name and password. Once logged in, you are provided with the operating system prompt; in the case of Linux or Unix, this will be either $ or %. You are then directly connected to an account on that system and can issue any commands you want. When you finish your work, you log out. This breaks the connection and returns you to the Telnet prompt on your own system. You can then quit Telnet with the quit command.

```
telnet> quit
```

When using Telnet to connect to a site that provides public access, you needn't provide a login name or password. Access is usually controlled by a series of menus that restrict what you can do on that system. If you are logging into a specific account on another system, you can use the -l option to specify the login name of that account.

## RSH, Kerberos, and SSH Remote Access Commands

The remote access commands were designed for smaller networks, such as intranets. They enable you to log in remotely to another account on another system and to copy files from one system to another. You can also obtain information about another system, such as who is logged on currently (see Table 15-3). Many of the remote commands have comparable network communication utilities used for the Internet. For example, rlogin, which remotely logs into a system, is similar to telnet. The rcp command, which remotely copies files, performs much the same function as ftp.

There are security risks with the use of remote operations like rcp, rlogin, and rsh (RSH package). Such commands allow easy unencrypted remote access to a Linux system. These commands should be used only within a local secure network. For Internet operations like these, you should use the secure versions of these commands provided by Kerberos and the Secure Shell (SSH), such as ssh, slogin, or scp (see Chapter 18). SSH commands are encrypted, providing a much higher level of security. Kerberos provides versions for Telnet, rlogin, rcp, rsh, and ftp, which provide authentication and encryption. The Kerberos versions operate using the same commands and options as the originals, making their use transparent to the user. If you install Kerberos on your system, Red Hat configures the user PATH variable to access the Kerberos versions of the remote commands, located at /usr/kerberos/bin, instead of /usr/bin.

You can use several commands to obtain information about different systems on your network. You can find out who is logged in, get information about a user on another system, or find out if a system is up and running. For example, the rwho command functions in the same way as the who command. It displays all the users currently logged into each system in your network

```
$ rwho
violet robert:tty1 Sept 10 10:34
garnet chris:tty2 Sept 10 09:22
```
