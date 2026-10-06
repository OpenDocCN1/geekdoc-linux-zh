NOTE: To configure Samba from a Mac OS client, edit the /etc/samba/smb.conf file (as root user). In a shared directory, add the line guest=yes (allow guest access to the share). You can also set encrypt passwords=no to accept clear-text passwords. Because encrypt passwords is a global setting, and newer Windows systems prefer encrypted passwords by default, you may only want to set that value if you have only Mac clients on your network.

# Sharing applications

Most UNIX-like systems rely on the X Window System (also referred to as X11 or simply X) to display over a network. Sharing applications over the network with X requires little more than having X running and making it to be directed to your display (see Chapter 3 for information on launching X applications).

Although the default graphical interface for Mac OS is a facility called Aqua, there is now an X11 for Mac OS available for users. The latest version of Mac OS includes a native installation. You must choose a Custom install or upgrade when you install Mac OS to get the X packages on your system. For further information on the X Window System in Mac OS, go to http://www.apple.com/macos/features/x11. To download your own copy of X11 for Mac OS, visit this site:

http://www.apple.com/downloads/macos/macos_updates/x11macos.html

When I checked the site you mentioned, they did not have the latest version of X11 available. For my new Mac Mini, I was able to install X11 from the installation disks that came with the computer. Open DVD D1 and select the Optional Installs package. Under applications, select the X11 package.

With X11 installed and running on your Mac OS, you can run the same X applications on Linux systems. However, you can also launch X applications from your Linux system and have them appear on your Mac OS desktop. From my Mac Mini (Mac OS 10.4.8), I did the following to start X and display an application from Fedora on my Mac desktop:

+   1. Start X11 on the Mac (from the Finder bar, select Go → Applications → X11), X11 starts and opens a Terminal.

+   2. From the Terminal window on the Mac, use the xhost command to tell X11 that it's okay to display an application from your Fedora machine. For example, to open permission to display X clients from the Fedora machine at IP address 10.0.0.100, type the following:

```
$ xhost + 10.0.0.100
```

+   3. Open a Terminal window on the Fedora machine and set your DISPLAY variable to the X11 instance on the Mac machine. For example, if you started X11 on a machine located at the address 10.0.0.50, you could identify the first X11 display on that computer by typing the following from the Terminal on your Fedora system: