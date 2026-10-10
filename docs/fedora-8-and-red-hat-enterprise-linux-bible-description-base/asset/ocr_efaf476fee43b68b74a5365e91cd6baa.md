The optional **xconfig** command can be used to configure your monitor and video card. If you use the **skipx** command instead (as shown in the following code sample), no X configuration is done. (After the system is installed, run **system-config-desktop** to set up your X configuration.) When you use the **xconfig** command, you can identify the type of X server to use based on your video card (`--card`) and monitor speed (`--hysync` and `--vsvnc`). A handful of other options enable you to set the color depth in bits (`--depth`), the screen resolution (`--resolution`), whether the default desktop is GNOME or KDE (`--defaultdesktop`), whether the login screen is graphical (`--startx` or `--startkboot`), and the amount of RAM on your video card (`--video ram`). (All the information after **xconfig** should actually appear on one line.)

```
skipx
```

or

```
xconfig --card="NVIDIA GeForce FX (generic)" --videoram=131072 \
--hysync=31.5-37.9 --vsvync=50-70 --resolution=800x600 \
--depth=16 --startxkboot --defaultdesktop gnome
```

The optional **network** command lets you configure your Fedora or RHEL system's interface to your network. The example tells your computer to get its IP address and related network information from a DHCP server (`--bootproto dhcp`). If you want to assign a particular IP address, use the `--bootproto static` option. Then change the IP address (`--ip`), netmask (`--netmask`), IP address of the gateway (`--gateway`), and IP address of the DNS server (`--nameserver`) to suit your system. You can also add a hostname (`--hostname`).

> **NOTE:** Although the **network** values appear to be on three lines, all values must be on the same line.

```
network --device eth0 --bootproto dhcp
```

or

```
network --device=eth0 --bootproto static --ip=192.168.0.1 \
--netmask 255.255.255.0 --gateway 192.168.0.1 \
--nameserver 192.168.0.254 --hostname duc.example.com
```

The **roothpw** command sets the password to whatever word follows (in the following example, **passWord**). It is a security risk to leave this password hanging around, so you should change this password (with the **passwd** command) after Linux is installed. You also have the option of adding an encrypted password instead (`--iscripted g.UJ.RQeOY3Bg -enablemd5`).

```
roothpw passWord
```

or

```
roothpw --iscripted g.UJ.RQeOY3Bg -enablemd5
```

The **firewall** command lets you set the default firewall used by your Fedora or RHEL system. The default value is **enabled** (if the firewall is turned on). You can also set **firewall** to **disabled** (no firewall). (These values are described in the installation