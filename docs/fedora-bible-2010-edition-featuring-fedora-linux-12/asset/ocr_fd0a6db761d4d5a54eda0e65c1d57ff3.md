The required keyboard command identifies a United States (us) keyboard by default. More than 70 other keyboard types are supported. (Run `system-config-keyboard` to see a list of available keyboard types.)

```
```
keyboard us
```
```

The optional xconfig command can be used to configure your monitor and video card. If you use the skipx command instead (as shown in the following code sample), no X configuration is done. (After the system is installed, run `system-config-display` to set up your X configuration.) When you use the xconfig command, you can identify the type of X server to use based on your video card (`--xcard`) and monitor specs (`--hysync` and `--vysync`). A handful of other options enable you to set the color depth in bits (`--depth`), the screen resolution (`--resolution`), whether the default desktop is GNOME or KDE (`--defaultdesktop`), whether the login screen is graphical (`--startxonboot`), and the amount of RAM on your video card (`--videoram`). (All the information after `xconfig` should actually appear on one line.)

```
```
skipx
```
```

or

```
```
xconfig --card="NVIDIA GeForce FX (generic)" --videoram=131072
        --hysync=31.5-37.9 --vysync=50-70 --resolution=800x600
        --depth=16 --startxonboot --defaultdesktop gnome
```
```

With most modern hardware, you don’t need to set up either of these commands, as Fedora will automatically configure the video card and monitor in most cases.

The optional network command lets you configure your Fedora system’s interface to your network. The example tells your computer to get its IP address and related network information from a DHCP server (`--bootproto dhcp`). If you want to assign a particular IP address, use the `--bootproto static` option. Then change the IP address (`--ip`), netmask (`--netmask`), IP address of the gateway (`--gateway`), and IP address of the DNS server (`--nameserver`) to suit your system. You can also add a hostname (`--hostname`).

> **NOTE:** Although the `network` values appear to be on three lines, all values must be on the same line.

```
```
network --device eth0 --bootproto dhcp
```
```

or

```
```
network --device=eth0 --bootproto static --ip=192.168.0.1
        --netmask 255.255.255.0 --gateway 192.168.0.1
        --nameserver 192.168.0.254 --hostname duck.example.com
```
```

Again, with most modern hardware, you normally don’t need the `network` command.

The rootpw command sets the password to whatever word follows (in the following example, `password`). It is a security risk to leave this password hanging around, so you should change