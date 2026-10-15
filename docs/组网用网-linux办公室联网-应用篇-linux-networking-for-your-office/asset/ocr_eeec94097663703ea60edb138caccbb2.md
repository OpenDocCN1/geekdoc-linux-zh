You can also use -q in conjunction with -f to locate the package that owns a specific file. For instance, suppose you want to uninstall the package that owns the file /usr/sbin/nmbd. Here’s what you might type, and see in response:

```
[root@speakerr root]# rpm -qf /usr/sbin/nmbd
samba-2.0.5a-1
```

If you’re sure you want to delete Samba, you could then do so by typing:

```
rpm -e samba
```

# Using the gnorpm Program

Using rpm from the command line is definitely the most flexible way to manage RPM files on your system. You might want to work with a GUI interface, though, either because you’re more comfortable with that or because you want to browse through available packages—either those already installed on your system or those on a CD or in some directory on your hard disk. In these circumstances, you can use the gnorpm program.

# NOTE

Prior to version 6.0, Red Hat Linux used the glint program rather than gnorpm, and some distributions may still use glint, or some other GUI front-end to rpm. If you type gnorpm and don’t get the program, try glint instead, or check your distribution’s documentation. If you use glint, the details of operation differ, but many of the basic principles are the same.

When you start gnorpm, you’re greeted by the Gnome RPM window shown in Figure 23.1. This window contains two panes. The left pane shows a hierarchical classification of installed package categories, and the right pane shows the packages that are installed in a selected category.

# NOTE

The hierarchical organization of installed packages doesn’t correspond to the organization of files in the Linux directory structure. The gnorpm hierarchy exists only to help you locate packages. In fact, because each RPM maintainer must classify his or her own RPM, the classification scheme tends to be confusing and inconsistent, so you may have to look several places to find a specific package.