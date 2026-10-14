Obviously, tweak this sample configuration so that it matches the settings on your particular network, and then start the DHCP server by typing sudo service dhcp3-server start. You should see

```
$ sudo service dhcp3-server start
* Starting DHCP server dhcpd3                    [OK]
```

If the service fails to start because of an error in the configuration file, you should see a reference to the error in the output on the screen. Track down that line in the dhcpd.conf file and look for missing semicolons at the end of lines or any other syntax errors you might have made.

# TFTPD

Once the DHCP server is set up, the next step is to install a TFTPD service on your PXE boot server. Type

```
$ sudo apt-get install tftpd-hpa
```

and APT will pull down the TFTPD server and the openbsd-inetd package it depends on. As this service is managed by inetd, it will be started only when a user accesses UDP port 69 on this machine. The firewall is disabled by default in my Kickstart and preseed examples, but if you have enabled it, be sure to open a port for UDP port 69.

# Configure Px elinux

Now that TFTPD is installed, you are ready to install and configure pxelinux. Pxelinux is a component of the syslinux package that provides a boot loader for CD-ROMs (including Ubuntu) called isolinux, a standard boot loader known as syslinux, and a PXE boot loader called pxelinux. While you could install the syslinux package and copy the files yourself, Ubuntu has already provided a netboot configuration ready for you to use on its mirrors. All you have to do is go to the TFTPD root directory and then download and extract the netboot tarball for your Lucid version. For instance, here are the steps to grab a netboot tarball for Lucid Lynx:

```
$ sudo cd /var/lib/tftpboot
$ sudo wget http://us.archive.ubuntu.com/ubuntu/dists/lucid/main/
installer-i386/current/images/netboot/netboot.tar.gz
$ sudo tar -xzvf netboot.tar.gz
```