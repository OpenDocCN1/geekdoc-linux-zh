# Access Variable Data Files in the /var Directory

The /var directory contains subdirectories used by various system services for spooling and logging. Many of these variable data files, such as print spooler queues, are temporary, whereas others, such as system and kernel logs, are renamed and rotated in use. Incoming electronic mail is usually directed to files under /var/spool/mail.

Linux also uses /var for other important system services. These include the top-most File Transfer Protocol (FTP) directory under /var/ftp (see Chapter 22, "Remote File Serving with FTP"), and the Apache web server’s initial home page directory for the system, /var/www/html. (See Chapter 19, "Apache Web Server Management," for more information on using Apache.)

# Logging In to and Working with Linux

You can access and use a Linux system in a number of ways. One way is at the console with a monitor, keyboard, and mouse attached to the PC. Another way might be via a serial console, either by dial-up via a modem or a PC running a terminal emulator and connected to the Linux PC via a null modem cable. You can also connect to your system through a wired or wireless network using the telnet or ssh commands. The information in this section shows you how to access and use the Linux system using physical and remote text-based logins.

> **NOTE**
> This chapter focuses on text-based logins and use of Linux. Graphical logins and using a graphical desktop are described in the section "Starting X" in Chapter 6.

# Text-based Console Login

If you sit down at your PC and log in to a Linux system that has not been booted to a graphical login, you see a prompt similar to this one:

```
```
Fedora Core release 3 (Heidelberg)
Kernel 2.6.10-1.760_FC3 on an i686

login:
```
```

Your prompt might vary, depending on the version of Fedora Core you are using. In any event, at this prompt, type in your username and press Enter. When you are prompted for your password, type it in and press Enter.

> **NOTE**
> Note that your password is not echoed back to you, which is a good idea.