# Terminal Consoles

> exam watch
> Even though it should be trivial for most Linux users, a part of one RHCSA objective is to “access a shell prompt.” You should now know how to set up access to different shell prompts.

By default, six command line consoles are available on RHEL systems. They're defined by the start-ttys.conf file in the /etc/init directory. Take a look at that file. You'll see that consoles are defined for runlevels 2, 3, 4, and 5. Active consoles are defined as device files /dev/tty1 through /dev/tty6. When a GUI is configured, it takes /dev/tty1. It's possible to configure more

virtual consoles, limited by those allowed for the root administrative user in the /etc/security file.

Normally, to change between consoles, press ALT and the function key associated with the console. For example, the ALT+F2 key combination moves to the second console. However, in the RHEL GUI, the ALT+F2 key combination is used to start the Run Application tool; therefore, you'll need to press CTRL+ALT+F2 to move to that second virtual console.

At a text console login, you'd see the following prompt, which depends a bit on the release of RHEL, the version number of the kernel, and the system hostname:

```
```
Red Hat Enterprise Linux release 6.0 (Santiago)
Kernel 2.6.32-71.el6.x86_64 on x86_64

server1 login:
```
```

The graphical login, which requires the installation of the GNOME Display Manager (GDM), is more intuitive, as shown in Figure 3-1.

# GUI Shell Interfaces

Once logged in to the GUI, access to the bash shell is easy. If you're in the default GNOME desktop environment, click Applications | System Tools | Terminal. Traditionally, administrators have worked from the console. But in many cases, working the command line from the GUI can be helpful, especially with the consoles that can be placed side by side. A right-click on a GUI terminal screen supports opening of additional terminals in different windows or in tabs. It also supports copy and paste as needed.

The screenshots of the command line taken for this book are based on the GUI-based command line, in part because dark text on a white screen is easier to read.