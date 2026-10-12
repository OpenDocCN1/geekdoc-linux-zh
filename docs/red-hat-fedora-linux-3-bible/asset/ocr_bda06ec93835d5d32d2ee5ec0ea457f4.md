```
`cdrom`
```

The required `lang` command sets the language (and to be more specific, the country as well) in which Fedora is installed. The value is U.S. English (`en_US_UTF-8`) by default.

```
`lang_en_US_UTF-8`
```

You can install multiple languages to be supported in Fedora. Here is an example of the default being set to U. S. English:

```
`langsupport --default en_US_UTF-8 en_US_UTF-8`
```

The required `keyboard` command identifies a United States (us) keyboard by default. More than 70 other keyboard types are supported.

```
`keyboard_us`
```

The optional `xconfig` command can be used to configure your monitor and video card. If you use the `skipx` command instead (as shown in the following code sample), no X configuration is done. (After the system is installed, run `system-config-display` to set up your X configuration.) When you use the `xconfig` command, you can identify the type of X server to use based on your video card (`--card`) and monitor specs (`--hsync` and `--vsync`). A handful of other options enable you to set the color depth in bits (`--depth`), the screen resolution (`--resolution`), whether the default desktop is GNOME or KDE (`--defaultdesktop`), whether the login screen is graphical (`--startxno`), and the amount of RAM on your video card (`--videoram`). (All the information after `xconfig` should actually appear on one line.)

```
```
skipx
or
xconfig --card="ATI Mach64 3D Rage IIC" --videoram=2048 --hsync=30-95
--vsync=50-180 --resolution=800x600 --depth=16 --startxno
 defaultdesktop=GNOME
```
```

The optional `network` command lets you configure your Fedora system’s interface to your network. The `network` tells your computer to get its IP address and related network information from a DHCP server (`--bootproto=dhcp`). If you want to assign a particular IP address, use the `--bootproto=static` option. Then change the IP address (`--ip`), netmask (`--netmask`), IP address of the gateway (`--gateway`), and IP address of the DNS server (`--nameserver`) to suit your system. You can also add a hostname (`--hostname`).

> NOTE: Although the `network` values appear to be on three lines, all values must be on the same line.

```
```
network --device eth0 --bootproto dhcp
or
network --device=eth0 --bootproto=static --ip=192.168.0.1
 --netmask=255.255.255.0 --gateway=192.168.0.1
 --nameserver=192.168.0.254 --hostname=duck.ab.com
```
```