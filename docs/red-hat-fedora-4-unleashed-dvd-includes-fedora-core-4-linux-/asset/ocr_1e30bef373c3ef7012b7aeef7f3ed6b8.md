Fedora uses GNOME's user-friendly suite of clients to provide a consistent and user-friendly desktop. GNOME is a staple feature of Red Hat's commercial Linux distributions and Fedora because Red Hat actively supports its development. GNOME clients are found under the `/usr/bin` directory, and GNOME configuration files are stored under the `/etc/gnome` and `/usr/share/gnome` directories, with user settings stored in the home directory under `.gnome`.

# Ximian GNOME for Red Hat

In 1999, Miguel de Icaza and Nat Friedman, the original GNOME developers, created a company and a product now known as Ximian. Ximian is a polished GNOME environment that offers not only an updated suite of GNOME clients, but also groupware software that provides integrated mail, calendar, addressing, and instant messaging services.

In August 2003, Ximian was acquired by Novell, Inc. The Ximian GNOME distribution, now named Ximian Desktop 2, is not included with Red Hat's Linux distros or Fedora, but you may be able to install it via CD-ROM or, if you have broadband access, in about an hour or less over the Internet. Versions are available for many different Linux distributions (even those on non-Intel platforms).

To get started, you can go to Novell's Ximian Desktop website at `http://www.novell.com/ products/desktop/download.html`. You first use `wget` to quickly download a graphical installer, which is then used to select a download site, selected files, and the base Ximian distribution. The download and installation are done as an automatic process, and Ximian replaces your default GNOME software with its own GNOME distribution. After installation, you can quickly install updates and bug fixes by using an update icon on the Ximian desktop.

A representative GNOME desktop, running the `gconf-tool-2` client used for setting themes, is shown in Figure 6.10.

![](bbox=[0.29, 0.61, 0.71, 0.87])

**FIGURE 6.10** Fedora's GNOME desktop uses the `metacity` window manager and offers a selection of GNOME (and KDE) themes.