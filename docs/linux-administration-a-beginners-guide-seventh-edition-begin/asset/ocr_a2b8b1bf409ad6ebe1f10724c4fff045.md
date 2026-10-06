# APPENDIX B Demo Virtual Machine 799

+   1. If you get a warning about the authenticity and fingerprint of the remote host, type yes to continue.

+   2. Enter root's password (72erty712) when prompted for the password.

+   3. Once logged in successfully, you'll be at the shell prompt of the Demo VM, where you can run numerous commands. For example, to view or change the hostname of the Demo VM using systemctl hostname, type

```
root@fedora-server # hostnamectl set-hostname "kick-ass-server"
--static
```

+   4. Use the exit to log out.

+   5. Use SSH to log back into the system formerly known as Demo VM to see your new hostname:

```
[you@client ~]$ ssh root@192.168.1.202
```

After logging in successfully, the new prompt should look like this:

```
[root@kick-ass-server ~]#
```

That's it!

# Cockpit Application

The latest Fedora distributions ship with the web-based Cockpit management console installed and enabled by default. Cockpit provides a web-based interface to aid system management. The Cockpit project is still somewhat in its infancy but is very usable and production ready in its current form. You can expect that a lot of new features and capabilities will be added over time.

As we've alluded throughout this book, there's nothing like the good ol' line to get your system/network admin tasks done quickly and efficiently. Forget about all these new GUI-based "point and click" tools to Cockpit like Cockpit.

But darn, when we were all pushed to dislike it, it turns out Cockpit has a web-based console built into it!

The Demo VM that you imported has its own Cockpit instance running and listening for connection requests on the default port 9090. Remember that, once fired up, the Demo VM is just like any other physical machine on your LAN. After, you can connect and access its services remotely.

To connect and use Cockpit, you will need to know the current IP address of the Demo VM. The IP address might even be printed for you at the login console/screen. You can view the login console/screen of the Demo VM using any of the methods discussed in the previous sections. Assuming that you discovered the IP address of the Demo VM (and that's 192.168.1.202) from any system within