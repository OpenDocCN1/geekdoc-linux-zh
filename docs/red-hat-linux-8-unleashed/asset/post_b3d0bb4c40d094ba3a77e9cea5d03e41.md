
stale files each day. (A stale file is any file not used after 10 days.) Red Hat Linux is configured by default to check /tmp each day in your system's scheduling table, /etc/crontab.

## Available Data Files in the /var Directory

The /var directory contains subdirectories used by various system services for spooling and logging. Many of these variable data files, as print spooler queues, are temporary, whereas others, such as system and kernel logs, are renamed and rotated in use. Incoming electronic mail is usually directed to files under /var/spool/mail.

Red Hat Linux also uses /var for other important system services. These include the top-most File Transfer Protocol (FTP) directory under /var/ftp (see Chapter 18, "Secure FTP Service"), and the Apache server's initial home page directory for the system, /var/www/html. (See Chapter 16, "Apache Web Server Management"), for more information using Apache.

## Logging into and Working with Linux

You can access and use a Red Hat Linux system in a number of ways. One way is at the console with a monitor, keyboard, and mouse attached to the PC. Another way might be via a serial console, either by dial-up via a modem or a PC running a terminal emulator connected to the Linux PC via a null mode console. You can connect to your system through a wired or wireless network using the telnet or ssh commands. The information in this section of the chapter shows how to access and use the Red Hat Linux system using physical and remote text-based logins.

> NOTE
> This chapter focuses on text-based logins and use of Linux. Graphical logins using a graphical desktop are described in the section "Starting X" in Chapter 6, "The X Window System."

## Text-based Console Login

If you sit down at your PC and log in to a Red Hat Linux system that has not been booted to a graphical login, you see a prompt similar to this one:

```
Red Hat Linux release 7.3.94 (null)
Kernel 2.4.18-11 on an i686
login:
```

Your prompt might vary, depending on the version of Red Hat Linux you're using. In any event, at this prompt, type in your username and press Enter. When you are prompted for your password, type it in and press Enter.

## Working with Virtual Consoles

> NOTE
> Note that your password is not echoed back to you, which is a good idea.

After logging in, you will be an interactive command prompt known as a *shell* in the Linux text-based or *console* mode.

While you're sitting at your command prompt, you can also use one or more *virtual* consoles or terminals. Virtual consoles allow you to log in to Red Hat multiple times (Each login is called a *session*). This can be useful if you are not using Red Hat's graphical desktop, but want to use several interactive programs, such as a text editor and Web browser, at the same time. To do so, after log in, run a program and jump to another login prompt, log in, and start another session. Red Hat Linux has 63 virtual consoles, but only the first 6 are configured for use. (You can use 7 if you don't run X11.)

- 1. Log in. You'll be using the first virtual console, or vt1 by default.
- 2. Press F2. You should then see another login prompt. Log in again, and you are then using vt2, the second Linux console.
- 3. Press Alt+F1 to jump back to vt1.
- 4. Press Alt+F2 to jump back to vt2.

You can jump back and forth between sessions using the Alt key plus the F key number of the desired session, such as F3, F4, F5, or F6.

One caveat when using virtual consoles is that there is a default limit on the available number (usually six) if an active X window is occupying vt. To jump to a virtual console from an X session, press Ctrl+Alt+F; it will be vt2. You can then jump back to your X session from the text-console by pressing Alt+F7 (to go to vt, in use by X). You should also be careful to save any work before you exit session, and log out of each session when finished. If you do not, you could leave an open login and shell prompt at the keyboard to anyone who walks by!

> NOTE
> In addition to virtual console keystrokes, the Linux console might also recognize the three-fingered salute (or Vulcan neck pinch), Ctrl+Alt+Del. This behavior (and the number of virtual terminals) can be controlled by the system administrator by editing the system's *initialization table*, `/etc/inittab`. See the Keyboard and Console HOWTO at http://www.tdlp.org/ for more details.

## Using Simple Keyboard and Mouse in a Linux Console Session

Working with Red Hat Linux in a console-based session usually involves entering commands from the keyboard. However, you can also use simple mouse controls as well. Linux keyboard combinations and mouse help provide virtual console navigation, start special system actions (such as rebooting or shutting down), provide shortcuts to save typing, and can aid in reading files or viewing program output.

For example, you can scroll the contents of your screen by pressing Shift+PageUp or Shift+PageDown, and copy and paste text using your mouse buttons. This section shows you how to access or default menus at the console, which can be helpful to get system information.
```
