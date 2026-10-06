# GUI User Managers

The obvious advantage to the GUI tool is it is usually just a point-and-click affair. Many of the Linux distributions come with their own GUI user managers. Fedora, CentOS, and RHEL come with a utility system-config-users, and openUSE/SEL Linux has YaST module that can be invoked with yast2 users. Ubuntu uses a tool Users Account, which is bundled with the gnome-controlcenter system applet. All these tools allow you to add, edit, and maintain the users on your system. These GUIs work fine—but you should be prepared to change user settings manually if you do not have access to the pretty GUI-ends. These interfaces can be found in the System -> Administration menu within the GNOME or KDE desktop environment. They can also be launched from the command line.

To launch your GUI user manager, you'd type this:

```
[root@fedora-server ~]#$ system-config-users
```

A window similar to the one in Figure 5-2 will open. In openSU or SLE, to launch the user management YaST module (Figure 5-3), you'd type this:

```
opensense-server:~ #$ yast2 users
```

In Ubuntu, to launch the user management tool (Figure 5-4), you'd type this:

```
master@ubuntu-server:~$ gnome-control-center user-accounts
```

![](bbox=[0.147, 0.573, 0.852, 0.913])

Figure 5-2 Fedora User Manager tool