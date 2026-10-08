# 130 CONFIGURATION AND ADMINISTRATION

When modifying getty settings you may be unable to log in; therefore you should always have an emergency boot floppy available. Another solution is to run at least one virtual console with an older version or a completely different getty. As a simple alternative, you could use the program getty or the internal getty of the System V init.

The use of a larger number of getty programs is not recommended on the one hand, many processes need RAM memory and on the other hand, the password must be entered again at each login. With the program open, any program can be started on an additional virtual console without having to log in or start a new getty.

# 4.9.1 The aget program

The getty program has been developed by W. Z. Venema and ported to LINUX by Peter Ørbæk. It is distributed with the util-linux collection by Rik Fait and is a relatively simple getty. This reduces the possible errors during installation, but makes the application relatively inflexible. The use of getty on virtual consoles in combination with simpleinit with problems. However, when connecting serial terminals or dialling in via modem, other getys are often more suitable.

The getty program should only be used in combination with simpleinit, since the correct setting of the environment variable TERM is carried out by init. Expected parameters are the baud rate of the connected device and the tty to be used. The order of parameters should play no role in this getty. The following example shows the use of getty in combination with simpleinit for a virtual console and a directly connected vt100 terminal.

```
tty:linux:/sbin/getty 9600 tty
tty1:vt100:/sbin/getty -L 19200 ttys1
```

In front of the login prompt, the file /etc/issue is displayed unless the -i option was specified. In the display, some special character sequences are substituted with the corresponding values so that, for example, the current kernel version could be shown. The complete list of possible variables is shown in Table 4.8.