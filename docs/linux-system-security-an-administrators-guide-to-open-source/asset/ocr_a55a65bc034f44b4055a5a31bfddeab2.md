The third module in the stack is pam_nologin. This is also an auth-only module type that accepts no arguments. Its purpose is to check for the existence of `/etc/nologin`. If `/etc/nologin` exists, then no users, except root, are allowed to log in; if `/etc/nologin` contains a message, it is displayed. For example, if `/etc/nologin` is

```
System down for maintenance until 2/28/99 at 4pm
```

then Example 5-9 exhibits the system's behavior when the user `joe` attempts to telnet to the system.

# **Example 5-9** Attempted Login with the Presence of `/etc/nologin`

```
$ telnet livfreddie
Trying 10.1.1.1...
Connected to livfreddie.
Escape character is '^]'.
Red Hat Linux release 5.2 (Apollo)
Kernel 2.0.36 on an i686
login: joe
Password:
System down for maintenance until 2/28/99 at 4pm
Login incorrect
login:
```

# **OH, BY THE WAY...**

> Did you ever wonder about how to get rid of the message that appears when you connect to a system? In Example 5-9, it is the two-line message beginning with “Red Hat Linux”? This message gives away information about your system, which does not reflect good security practice. On Red Hat 5.2/6.0, the message displayed reflects the contents of `/etc/issue.net` for remote connections and `/etc/issue` for local connections. At this point, you may be tempted to rush off and modify these files to suit your needs. Don't. The files are rewritten at every reboot! In order to modify these files, you must modify `/etc/rc.d/rc.local` or `/etc/rc2.d/S991local` is a symbolic link to `/etc/rc.d/rc.local`, which is executed upon entering run level 2. Be sure to replace this message with something appropriate, maybe something like “This is a restricted system. All activities are logged.” But whatever you do, don't reveal the operating system, hardware, or other information that may be used against you. And don't use words like “Welcome”! There are many other ways to replace this message, some of which will be discussed at various points in this text.

By default, Joe will actually be able to attempt to log in three more times, but of course the result will be the same. Existing login sessions are not affected by the `/etc/nologin` file.

This file is normally used for purposes of system maintenance, but it also is beneficial in case of a system breach. This topic is discussed in Chapter 3.

Normally, the `/etc/nologin` file does not exist and the user, once authenticated, will be granted access. The subsequent modules in `/etc/pam.d/login` are then invoked.