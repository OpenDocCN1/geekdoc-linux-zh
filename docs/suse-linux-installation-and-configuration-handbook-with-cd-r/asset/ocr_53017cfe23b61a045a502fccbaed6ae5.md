3. Issue the command isapnp /etc/isapnp.conf. This command will try to configure the PnP devices specified in the configuration file with the specified parameters.

# CAUTION

You might be faced with one of the following cases when applying isapnptools:

+   - Your system locks up when using pnpdump -c.
+     You'll have to generate the file without the -c parameter and edit the isapnp.conf file yourself.
+   - Your system locks up on isapnp.
+     You'll have to reboot. If your system locks up when you start the system, use the SuSE emergency system on the SuSE installation media, mount your Linux partition, and edit the isapnp.conf file.
+   - isapnp outputs a fatal error.
+     The resources listed in the isapnp.conf file are already in use. In most cases, they are already used by the device you want to assign the resources to. Reboot and if you get the same error at system start, you will have to edit the isapnp.conf file manually.

# TIP

You can use the SuSE Emergency System at any time to mount a system with boot up problems. In SuSE 6.3, you should boot using the second CD (Text based).

Boot from the Linux installation media or use the setup.exe to start the installation process. Boot the SuSE Emergency System. It should boot to a login prompt. Log in as root and enter the following:

```
bash#mount /dev/(Your Linux Partition) /mnt
bash#cd /mnt/etc
bash#vi isapnp.conf or bash#mv isapnp.conf isapnp.bak
```

# Editing the isapnp.conf File

Throughout this book, you'll find many sections about editing the isapnp.conf file. In each chapter that we mention isapnp.conf, we'll be interested only in setting the device discussed by the chapter. So, if you find some devices in your isapnp.conf file without configuration, either look in the file you just backed up (isapnp.conf.bak) or look up the configuration procedures of the device in the corresponding chapter.

Here is a sample section from the isapnp.conf file:

```
1 # [ Start of the configuration of the 1. logical device on the 1. ISA PnP card ]
2 # Multiple choice time, choose one only !
3 # [ Now you are offered different configuration possibilities for LD 0 ]
4 # [ Each possibility is separated from the following by a blank line ]
```