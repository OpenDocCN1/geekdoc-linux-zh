The `/var/lib/dpkg/status` file shows the status of installed packages. The following is an example of this file:

```
Package: telnet
Status: install ok installed
Priority: standard
Section: net
Installed-Size: 176
Maintainer: Herbert Xu <herbert@debian.org>
Source: netkit-telnet
Version: 0.16-4
Replaces: netstd
Depends: libc6 (>= 2.1.2), libncurses5
Description: The telnet client.
The telnet command is used for interactive communication with another host
using the TELNET protocol.
```

Normally these files are used only by `dpkg`, but they can be viewed or searched for information on available and installed packages.

Even though the exam objectives require you to know how to edit these files, you will rarely do it. However, they can contain useful information about the packages installed and available on your system.

# # Using dselect

# ## 2.2 Installation and Package Management

+   * Use **Debian package management**. Use the Debian package management system, from the command line (`dpkg`) and with interactive tools (`dselect`).

The `dselect` tool is an overlay to `dpkg` that provides a character-based graphical interface to enhance ease of use. When you run `dselect`, it displays the screen shown in Figure 3-1.

![](bbox=[0.16, 0.73, 0.84, 0.87])

Debian GNU/Linux 'dselect' package handling frontend.

+ @. f@Access Choose the access method to use.
1. fU@update Update list of available packages, if possible.
2. fS@elect Request which packages you want on your system.
3. fI@n@all Install and upgrade wanted packages.
4. fO@nconfig Configure any packages that are unconfigured.
5. fL@remove Remove unneeded software.
6. fQu@it Quit dselect.

Move around with "^" and "^", cursor keys, initial letters, or digits;
Press center to confirm selection. "^L" redraws screen.

Version 1.6.14 (130c). Copyright (C) 1994-1996 Ian Jackson. This is free software: see the GNU General Public License version 2 or later for copying conditions. There is NO warranty. See dselect --license for details.

Figure 3-1: Main dselect menu