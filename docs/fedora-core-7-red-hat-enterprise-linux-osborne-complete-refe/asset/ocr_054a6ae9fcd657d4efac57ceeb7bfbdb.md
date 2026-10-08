# **Virtual Network Computing**

A VNC (Virtual Network Computing) installation lets you boot the installation normally on the install system, and then lets the installation be managed from another Linux host, stepping through the install system's installation screen. It is a kind of remotely controlled installation, over a network connection. A VNC install requires that the host computer be running a VNC server. This is managed by the `vncserver` script, which can be controlled with `system-config-services` (System | Administration | Server Settings | Services on the main menu). You can also use the **service** tool.

```
service vncserver start
```

Once vncserver is started, the host then becomes a VNC server that can access and control installations being performed on other systems. As the VNC server, the host uses the vncviewer client to interact with the installation process on the install system. The client is invoked with the **-listen** option that checks for reverse connections from a VNC server.

```
vncviewer -listen
```

The install system has to then start the installation procedure by specifying a VNC install at the boot prompt or the graphical menu options, and providing the host computer IP address along with a password.

```
boot: linux vnc vncconnect=192.168.0.2 vncpassword=geo4455
```

On the install system you will have to first configure your language, keyboard, and network connection. Once you have configured the network connection for your install system, then a connection can be made to the VNC server. You can then move to the VNC host system and continue installation from there.

# **Automating Installation with Kickstart**

Kickstart is a method for providing a predetermined installation configuration for installing Fedora. Instead of having a user enter responses on the install screens, the responses can be listed in a kickstart file the install process can read from. You will need to create a kickstart configuration file on a working Fedora system. (Kickstart configuration files have the extension **.cfg**.) A kickstart file is created for every Fedora system that holds the install responses used for that installation. It is located in the root directory at

```
/root/anaconda-ks.cfg
```

If you plan to perform the same kind of install on computers that would be configured in the same way, say on a local network with hosts that have the same hardware, you could use this kickstart file as a model for performing installations. It is a text file that you can edit, with entries for each install response, like the following for keyboard and time zone:

```
keyboard us
timezone America/Los_Angeles
```