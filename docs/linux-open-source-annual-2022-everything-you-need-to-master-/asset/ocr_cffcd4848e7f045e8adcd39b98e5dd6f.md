# # Distros

likely have made things easier. It’s worth noting that FreeBSD is planning on making direct UEFI booting available in a coming release.

# ## Installing software

FreeBSD offers two ways to get software. The first is the Ports Collection. If you included it during your installation, poke around the `usr/ports` directory. Alternatively, you can opt to install software pre-compiled as well. Each of these has their own pros and cons. Installing the pre-compiled packages is faster and potentially easier/less error-prone. However, building software on your machine will better tailor it for your hardware. The first step is to get the package tool set up on your system. Enter `pkg` in your shell, and if it’s not already present you’ll be prompted to download it. Your first step should be to update the package database:

```
```
pkg update
```
```

Then, search for your desired program with:

```
```
pkg search [your desired term]
```
```

To install something, use this:

```
```
pkg install [package name]
```
```

You’ll see the progress of the install in the terminal, including the calculation of dependencies, the download of all that software and the actual installation. If you need to backtrack, it’s just as simple:

```
```
pkg delete [package name]
```
```

You can see all the packages you have installed with:

```
```
pkg info
```
```

Again, if you’re a Linux user who regularly drops down a quick terminal to search and install software in Ubuntu or Fedora, it will take you all of 14 seconds to get the hang of this. And installing Ports is just as easy.

# ## Day-to-day usage

Using FreeBSD on a day-to-day basis is precisely as described in the previous section. You’ll find a lot of things very familiar as you’re navigating around the console. And of course, applications operate just the same on FreeBSD as they do on Linux. There are only two areas where a little adjustment will be required. The first is system configuration. While the `/etc/` directory exists and does indeed contain many configuration files, there’s a useful one that’s unique to FreeBSD. As you work with FreeBSD you’ll see references to making entries in the `rc.conf` file. This contains a smattering of important system-level settings. If you open it up, you’ll see some of the things you set during install (such as network config). It’s very short, but one would expect it to grow longer with your personal configuration.

The `bsdconfig` utility can help with some of these tasks, and it’s as close to a control panel as you’ll get without installing some sort of desktop that contains one. It’s a menu-driven terminal program not unlike the installer, where you use arrow keys and Tab to jump around the dialogue. It won’t be too much of an adjustment, as even some modern package systems will use these types of dialogues when configuring individual packages.

You should also expect to do a bit more troubleshooting on FreeBSD. To clarify, this isn’t because things in FreeBSD are broken, but rather there are things that FreeBSD does differently by design that a Linux user will have to learn through research. A case in point: the `pkg` command does follow dependencies, but not quite in the way a Linux user might expect.

The author issued a quick `pkg install lnx` command, to which the output indicated that a number of packages would be installed. On completion the `startx` command failed with an error. Some quick checking revealed that the LXQt desktop was installed, but not Xorg was not. When the startup failed again after the X install, further poking around showed that while the base X server was there along with the top-level LXQt desktop, the Q16 toolkit that sits between them was still missing. And even when this was installed, using the `startx` command launched a default twm-based afloat.

![](bbox=[0.18, 0.46, 0.48, 0.61])

> > The installer’s ‘distributions’ are package sets. You only have a choice of adding up to seven of these sets as part of the installation.

# ## » FREEBSD’S LINUX COMPATIBILITY

While it may not be compatible with other BSDs, FreeBSD does come with a feature that enables you to run Linux software on it. The Linux Binary Compatibility layer allows you to install both 32 and 64-bit Linux applications, although it appears it supports for 1386-based software is fading. To add Linux compatibility, first add the Linux module for the FreeBSD kernel (while logged in as root):

```
```
kldload linux64
```
```

Then install the package (or build the port) for the emulation layer:

```
```
pkg install emulators/linux-c7
```
```

Add the following to `/etc/rc.conf/` (to make sure Linux compatibility is loaded at startup):

```
```
linux_enable="YES"
```
```

Then FreeBSD system is now set up to run Linux programs. Some other considerations you may need to take into account include:

+   * Does the program require any shared libraries? If so, you’ll need to track them down and install them as well.
+   * Does the program come in a particular package format? Some traditional packages such as .DEB or .RPM are easy enough to crack open, but newer ones like FlatPak (see LXFX244 for a deep dive) or Canonical’s Snap may not be as simple.
+   * See the handbook (www.freebsd.org/doc/handbook/linuxemu- lbc-install.html) to learn more about these and other topics.

![](bbox=[0.55, 0.78, 0.87, 0.95])

> > Before you log in, all the dmesg output will scroll by you furiously. Once you’re complete you end up with a prompt at the bottom of the screen.