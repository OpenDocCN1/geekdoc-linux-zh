
Starting graphical installation...

- Return to the desktop where you are going to view the install procedure. A VNC window should appear on the desktop containing the Fedora Welcome screen. Proceed with installation as you would normally.

> **NOTE:** If you are not able to connect to the viewer, make sure that port 5500 is open and accepting connections on your desktop system. Check the descriptions of iptables in Chapter 13 for further information on opening ports in your firewall.

## Performing a kickstart installation

If you are installing Fedora on multiple computers, you can save yourself some trouble by preconfiguring the answers to questions asked during installation. The method of automating the installation process is referred to as a *kickstart* installation. A kickstart file can not only be used to drive a regular Fedora installation, but can also be used to create Fedora Live CDs.

> **CAUTION:** Based on the information you provide in your `ks.cfg` file, kickstart will silently go through and install Fedora without intervention. If this file is not correct, you could easily remove your master boot record and erase everything on your hard disk. Check the `ks.cfg` file carefully and test it on a noncritical computer before trying it on a computer hiding critical data.

The general steps of performing a kickstart installation are as follows:

- **Create a kickstart file.** The kickstart file, named `ks.cfg`, contains the responses to questions that are fed to the installation process.
- **Install kickstart file.** You have to place the `ks.cfg` on a floppy disk or CD, on a local hard disk, or in an accessible location on the network.
- **Start kickstart installation.** When you boot the installation procedure, you need to identify the location of the `ks.cfg` file.

In the example in this chapter, you create your kickstart file directly with a text editor. If you prefer, you can use the Kickstart Configurator (`system-config-kickstart` command, from the package of the same name), which is a graphical tool for creating kickstart files.

## Creating the kickstart file

A good way to begin creating your kickstart file is from a sample `ks.cfg` file. When you install Fedora, the installation process places a file called `anaconda-ks.cfg` into the `/root` directory. You can use this file as the basis for the `ks.cfg` file that you will use for your kickstart installs.

The particular `/root/anaconda-ks.cfg` file you get is based on the information you entered during a regular installation (CD, NFS, and so on). Presumably, if you are installing Fedora on other computers for the same organization, multiple computers may have a lot of the same hardware and configuration information. That makes this a great file for you to start creating your `ks.cfg` file from.

> **NOTE:** For further details about how to use kickstart, refer to http://fedoraproject.org/wiki/Anaconda/Kickstart. To use a more graphical tool for configuring kickstart, run the system-config-kickstart command (after installing the package of the same name with the yum install system-config-kickstart command).

To start, log in as the root user. Then make a copy of the `anaconda-ks.cfg` file to work on.

```
# cp anaconda-ks.cfg ks.cfg
```

Use any text editor to edit the `ks.cfg` file. Remember that required items should be in order and that any time you omit an item, the user will be prompted for an answer. Entries from a `ks.cfg` file that was created from a regular DVD installation of Fedora are used as a model for the descriptions below. You should start with your own `anaconda-ks.cfg` file, and as a result, your file will start out somewhat differently. Commented lines begin with a pound sign (#).

The first uncommented line in the `ks.cfg` file should indicate whether the installation is an upgrade or an install. The `install` option runs a new installation. You can use the `upgrade` keyword instead to upgrade an existing system. (For an upgrade, the only requirements are a language, an install method, an install device, a keyboard, and a boot loader.)

```
install
```

The method of installation is indicated on the next line. Possible locations for the installation media include: NFS (nfs --server=servername --dir=installdir), FTP (url --url ftp://user:password@server/dir), HTTP (url --url http://server/dir), or hard drive (harddrive --dir=/dir --partition=/dev/partition). For the default DVD or CD install, you may see:

```
cdrom
```

Because the DVD or CD installation is the default, you may also see no method of installation.

The required `lang` command sets the language (and to be more specific, the country) in which Fedora is installed. The value is U.S. English (en_US.UTF-8) by default:

```
lang en_US.UTF-8
```

You can install multiple languages to be supported in Fedora. Here is an example of the default being set to U.S. English:

```
langs --default en_US.UTF-8 en_US.UTF-8
```

The required keyboard command identifies a United States (us) keyboard by default. More than 70 other keyboard types are supported. (Run `system-config-keyboard` to see a list of available keyboard types.)

```
keyboard us
```

The optional xconfig command can be used to configure your monitor and video card. If you use the skipx command instead (as shown in the following code sample), no X configuration is done. (After the system is installed, run `system-config-display` to set up your X configuration.) When you use the xconfig command, you can identify the type of X server to use based on your video card (`--xcard`) and monitor specs (`--hysync` and `--vysync`). A handful of other options enable you to set the color depth in bits (`--depth`), the screen resolution (`--resolution`), whether the default desktop is GNOME or KDE (`--defaultdesktop`), whether the login screen is graphical (`--startxonboot`), and the amount of RAM on your video card (`--videoram`). (All the information after `xconfig` should actually appear on one line.)

```
skipx
```

or

```
xconfig --card="NVIDIA GeForce FX (generic)" --videoram=131072 \
        --hysync=31.5-37.9 --vysync=50-70 --resolution=800x600 \
        --depth=16 --startxonboot --defaultdesktop gnome
```

With most modern hardware, you don’t need to set up either of these commands, as Fedora will automatically configure the video card and monitor in most cases.

The optional network command lets you configure your Fedora system’s interface to your network. The example tells your computer to get its IP address and related network information from a DHCP server (`--bootproto dhcp`). If you want to assign a particular IP address, use the `--bootproto static` option. Then change the IP address (`--ip`), netmask (`--netmask`), IP address of the gateway (`--gateway`), and IP address of the DNS server (`--nameserver`) to suit your system. You can also add a hostname (`--hostname`).

> **NOTE:** Although the `network` values appear to be on three lines, all values must be on the same line.

```
network --device eth0 --bootproto dhcp
```

or

```
network --device=eth0 --bootproto static --ip=192.168.0.1 \
        --netmask 255.255.255.0 --gateway 192.168.0.1 \
        --nameserver 192.168.0.254 --hostname duck.example.com
```

Again, with most modern hardware, you normally don’t need the `network` command.

The rootpw command sets the password to whatever word follows (in the following example, `password`). It is a security risk to leave this password hanging around, so you should change this password (with the `passwd` command) after Linux is installed. You also have the option of adding an encrypted password instead (--iscrypted).

```
rootpw password
```

or

```
rootpw --iscrypted                (line continues...)
$6$NtBq.5029fdfd412699$GfCCHdJEdPbgdc3.T/0e3hqNmqr1wMR/fYsd6rErFI3j0/dfGnOAS9QLj6nvb47PHjN.0UWZV3Ect.X3Md8B3jjJ1/B.
```

The firewall command lets you set the default firewall used by your Fedora system. The default value is enabled (if the firewall is turned on). You can also set firewall to disabled (no firewall). (These values are described in the installation procedure earlier in this chapter.) As you can see in the example, you can optionally indicate that there be no restrictions from host computers on a particular interface (--trust eth0). You can also allow an individual service (--service=ssh) or a particular port:protocol pair (--port 1234:udp).

```
firewall --enabled --trust=eth0 --service=ssh --port=1234:udp
```

The required authconfig command sets the type of authentication used to protect your user passwords. The --enablashadow option enables the /etc/shadow file to store your passwords. The --passalgo=sha512 option enables SHA512-based encryption for the passwords. (You would typically use both.)

```
authconfig --enablashadow --passalgo=sha512
```

The selinux command indicates whether or not Security Enhanced Linux is enabled. The following line shows it as enabled and enforcing:

```
selinux --enforcing
```

The timezone command sets the time zone for your Linux system. The default, shown here, is United States, New York (America/New_York). The --utc option indicates that the computer’s hardware clock is set to UTC time. If you don’t set a time zone, US/Eastern is used.

```
timezone --utc America/New_York
```

The bootloader command sets the location of the boot loader (GRUB, by default). For example, --location=mbr adds GRUB to the master boot record. (Use --location=none to not add GRUB.) The driveorder option describes which hard disk to look on first for the master boot record. You can also add kernel options to be read at boot time using the append option (--append hdd=ide=0) or an optional password for GRUB (--password=GRUBpassword).

```
bootloader --location=mbr --driveorder=sda --append="rhgb quiet" --password=GRUBpassword
```
