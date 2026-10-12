![](bbox=[0.23, 0.12, 0.71, 0.43])

**Figure 4-4**: You can install any other CDs you may have.

When you’re done with Firstboot, you’re really done for good because it runs only once when you boot for the first time. If, for some reason, you want to go through these steps again, here’s the scoop on how to run Firstboot again:

Log in as root and type the following commands in a terminal window (to open a terminal window, choose Main Menu→System Tools→Terminal):

```
rm /etc/sysconfig/firstboot
chkconfig --level 5 firstboot on
```

That’s it! Next time you reboot the PC, you have the pleasure of meeting Firstboot again. If you want to run Firstboot interactively from GNOME or KDE, you can do so by logging in as root and typing the following commands in a terminal window:

```
rm /etc/sysconfig/firstboot
firstboot
```

When you’re through with Firstboot, you get the graphical login screen (shown in Figure 4-5).

The login window in the middle of the screen displays a welcome message with your PC’s name — it’s called the host name. The name is assigned when the network is configured. The network isn’t configured, localhost.localdomain is the host name. If your PC gets its network address (the