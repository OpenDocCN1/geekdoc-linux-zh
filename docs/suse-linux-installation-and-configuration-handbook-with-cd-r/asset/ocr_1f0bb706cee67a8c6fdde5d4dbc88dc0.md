+   - **login.config**—This file describes how mgetty should behave if the user who dials in logs in successfully.
+   - **mgetty.config**—In this file, you should specify to which modems/ports mgetty should listen. Each modem or port can have its own configuration that should be used by mgetty.
+   - **voice.conf**—This file is used to configure your SuSE Linux as a voice answering machine.

In this chapter, we will discuss the first three files. In addition, one more configuration file exists that you should edit. You should add an entry to the /etc/inittab file to cause mgetty to start on system boot.

> **NOTE** mgetty is not a normal program that is run by hand. For mgetty to function correctly, it must be called by init. This requires mgetty to have an entry in the /etc/inittab file.

# Preparing inittab

As root, open the /etc/inittab in your favorite editor. SuSE Linux has prepared a default entry for mgetty around line 85 in SuSE Linux 6.3. The default entry is commented out; remove the comment hash and save the file. If you have lost the entry, it should look like the following:

```
mo:23:respawn:/usr/sbin/mgetty -s 38400 modem
```

The modem in the previous line represents the modem port on your system. If you have set up your modem using YaST as described in Chapter 23, you will have a /dev/modem symbolic link to your mode port. You can specify other ports to use by changing modem to the port your modem uses. The -s option sets the speed of this modem to 38400. In fact, setting up options for the modem in inittab is not recommended; you should use the /etc/mgetty+sendfax/mgetty.config to set options instead.

After you have edited the entry in /etc/inittab, you should activate this entry by issuing the following command as root:

```
bash#kill -1 1
```

# Preparing mgetty.config

The mgetty.config configuration file is organized with one global section followed by per port configuration sections, with the global configuration section coming first. A simple mgetty.config file should look like the following:

```
speed 38400 #set the speed to 38400 for all modems
rings 3 #answer after the third ring
port modem #modem on port /dev/modem
```