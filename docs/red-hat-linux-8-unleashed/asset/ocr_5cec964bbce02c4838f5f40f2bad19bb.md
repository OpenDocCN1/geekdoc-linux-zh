stale files each day. (A stale file is any file not used after 10 days.) Red Hat Linux is configured by default to check /tmp each day in your system's scheduling table,
/etc/crontab.

# Available Data Files in the /var Directory

The /var directory contains subdirectories used by various system services for spooling\and logging. Many of these variable data files, as print spooler queues, are temporary,
whereas others, such as system and kernel logs, are renamed and rotated in use. Incoming
eelectronic mail is usually directed to files under /var/spool/mail.

Red Hat Linux also uses /var for other important system services. These include the top-most File Transfer Protocol (FTP) directory under /var/ftp (see Chapter 18, "Secure FTP
Service"), and the Apache server's initial home page directory for the system,
/var/www/html. (See Chapter 16, "Apache Web Server Management"), for more information
using Apache.

# Logging into and Working with Linux

You can access and use a Red Hat Linux system in a number of ways. One way is at the
console with a monitor, keyboard, and mouse attached to the PC. Another way might be\via a serial console, either by dial-up via a modem or a PC running a terminal emulator
connected to the Linux PC via a null mode console. You can connect to your
system through a wired or wireless network using the telnet or ssh commands. The infor-mation in this section of the chapter shows how to access and use the Red Hat Linux
system using physical and remote text-based logins.

> NOTE
This chapter focuses on text-based logins and use of Linux. Graphical logins using a graphi-ncal desktop are described in the section "Starting X" in Chapter 6, "The X Window System."

# Text-based Console Login

If you sit down at your PC and log in to a Red Hat Linux system that has not been booted
to a graphical login, you see a prompt similar to this one:

```
Red Hat Linux release 7.3.94 (null)
Kernel 2.4.18-11 on an i686
login:
```

Your prompt might vary, depending on the version of Red Hat Linux you're using. In any
event, at this prompt, type in your username and press Enter. When you are prompted for
your password, type it in and press Enter.