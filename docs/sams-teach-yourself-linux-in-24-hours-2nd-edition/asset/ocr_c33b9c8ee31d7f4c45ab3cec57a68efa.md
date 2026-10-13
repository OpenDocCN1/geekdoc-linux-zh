# FIGURE 7.3

The xdm client is the X display manager and provides a login prompt to X.

![](bbox=[0.38, 0.13, 0.92, 0.48])

The initdefault line tells OpenLinux what run level to use by default. To boot directly to the xdm login screen, change the 3 to a 5, like this:

```
id:5:initdefault:
```

Save the file, exit your text editor, and either use the command /sbin/telinit 5 or reboot OpenLinux with the shutdown command. When you reboot to OpenLinux, you see the xdm screen, as shown in Figure 7.3.

> A nice alternative to xdm is the K Display Manager, or kdm. This client offers more login choices and configurations than the stock xdm client. For details about how to configure kdm, see the section “Configuring kdm” in Hour 8.

# X11 Window Managers

One of the great things about X11 is that you have freedom of choice in how you want to manage your windows and programs on your screen. All the hard work of screen management is done by a window manager, which is simply another X11 program or client. Of course, you don’t have to use a window manager with X. For example, create a file called .xinitrc in your home directory with a single line:

```
xterm
```