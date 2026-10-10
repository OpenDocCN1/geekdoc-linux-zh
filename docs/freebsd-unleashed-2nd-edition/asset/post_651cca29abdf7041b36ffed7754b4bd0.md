
## Reclaiming Hard Disk Space Used by the Port-Building Process

After you're done building and installing a port, the work directory is still sitting there, filled with the unpacked tree of source code and compiled binary objects. This can take up a fair amount of disk space. It's always advisable to clean this directory out after installation—returning the port to its original pristine state—by running one more `make` command, this time with the `clean` target:

```sh
# make clean
```

This deletes the work directory and everything in it. It also cleans out the port directory for each dependency listed. However, it does not remove the tarball files from `/usr/ports/distfiles`; you'll have to remove these files yourself.

> **TIP**
> Unless you really need the disk space, you might want to leave the tarballs intact in the `/usr/ports/distfiles` directory. You can save a lot of time this way—if you should ever need to rebuild or reinstall a port, the system can use the file it already has, instead of having to download it again.
>
> The beauty of ports is that if a security hole or critical bug is fixed in a port that you have installed, the ports collection might solve it by placing a patch file in the `files` directory of the port, not by bumping the revision number of the entire distribution file (and causing you to have to download a new tarball). A simple rebuild allows you to incorporate the new patch into your old sources.

Periodically, you may want to issue a top-level recursive `make clean` on the entire ports collection. There’s a makefile at both the `/usr/ports` level and the category level below it that enables you to do odd tasks such as building all the ports in a category at once (for example, building every "www" port by running `make` from inside `/usr/ports/www`). More usefully, it lets you clean every port at once, in one very long recursive process. You do this simply by going to `/usr/ports` and entering `make clean`. You can now go and get a sandwich if you want; like cleaning an oven, this process will be worthwhile but usually takes forever.

### When a Port Will Not Build: Searching for Solutions and Using Upgrade Kits

As convenient as the ports collection is, it’s not perfect—and with the amount of change that goes on in the tree, especially with so many ports (such as the ones related to GNOME and KDE) interrelated and constantly evolving, chances are that you’ll run into some stumbling blocks now and then. The general failure behavior is for the compile process to fail with "`*** Error code 1`" or a similar message. When this happens, you can try a number of things.

First, make sure you’re starting from a clean port. If there is a pre-existing work directory, it’s possible that you’ve mixed new sources with old, resulting in an unbuildable port. Run `make clean` to start over from a clean slate.

It’s also important to make sure you have the very latest ports tree available. If a port doesn’t build, chances are it’s a temporary condition that will have affected many other users besides yourself. A new version of the ported software might have been released since the version your ports refer to, for example, or perhaps your ports refer to a version that was newly released at the time your ports tree was installed, and some of the patches (written for a previous version) might have inadvertently become incompatible. If your ports tree is even a few days out of date, the chances are good that the port has been fixed in the meantime. Synchronize your ports tree as discussed earlier in this chapter and try building the port again (make sure you run `make clean` first).

If this doesn’t work, it’s time to seek outside assistance. Head to the FreeBSD Web site at `http://www.freebsd.org` and go to the Mailing Lists link, where you can search the relevant mailing lists. Make sure you check the Ports list as one of the search criteria. Then perform the search on the name of your port and some of the relevant text in the last few lines of the compiler output. If there’s anything commonly failing that other people have noticed, you’ll probably find something useful this way.

Still no luck? There’s one more good recourse: the port maintainer. Look in the port’s `Makefile` for the `MAINTAINER` variable, which is set to the e-mail address of the maintainer.

Send off a politely worded, undemanding e-mail containing the last (relevant) part of the compiler output, as well as information about your system (the output of `uname -a`, for instance). The maintainer is usually a very overworked, underappreciated individual, so be sure to express your gratitude for any help!

There may come a time when a port will fail to build, claiming that your system is “too old.” It will inform you that you either need to upgrade your entire system or install an upgrade kit. This latter option is much preferable; despite its name, it doesn’t upgrade your system at all, and it’s very nonintrusive.

An upgrade kit is a set of updated `include` files that the ports collection needs in order for its customized build targets to work. Most of these `include` files are in `/usr/ports/mk` and can therefore be brought up to date with `CVSup`. However, an unavoidable obstacle is that some required files are not within `/usr/ports`—they’re elsewhere in the core system, such as `/usr/share` or `/etc`. An upgrade kit is a standard FreeBSD package that provides newer versions of these files, enabling you to continue building ports even when your ports tree is much newer than your base system. You can install an upgrade kit using `pkg_add`, as with any package.

Upgrade kits are distributed from `http://www.freebsd.org/ports`, and there is one available for updating from any supported release version to the current spot in its corresponding `-STABLE` branch. You can install successive upgrade kits if you need to. However, it will eventually become necessary for you to upgrade your entire system, as you’ll learn in Chapter 17.

### Fresh Ports

The output of the `CVSup` synchronization process is a useful, but hardly ideal way to keep track of which ports have changed. There’s a very handy Web site (see Figure 14.5) that should be in the bookmarks or favorites of any FreeBSD administrator: Fresh Ports.

Maintained separately from the FreeBSD project proper, Fresh Ports is a database linked to the main CVS repository for the ports collection. It constantly monitors all check-ins and lists them in reverse chronological order. You can register with the Web site and set up a watch list for your favorite ports. You’ll be e-mailed whenever anything on your watch list changes, and you can view exactly what the changes are to each port so that you can determine whether the change is worth upgrading for. For instance, if a port is bumped up a version or a crucial security fix has been checked in, you may well want to upgrade; however, if the only recent change is to fix a typo in an installer error message, don’t bother.

![](img/48eec858cce7dfb89da36a4d40b7daf3_369_0.png)

FIGURE 14.5 The Fresh Ports Web site (www.freshports.org).

## CHAPTER 15 Printing

Setting up a printer in FreeBSD is one of the more complex topics you will have to deal with if you administer FreeBSD. Unfortunately, FreeBSD printing is not as simple as installing a driver, selecting the printer from a Control Panel, and then printing. Printing from FreeBSD involves configuring one or more configuration files and possibly installing filters if you need to print anything more advanced than plain text. After a basic outline of the major printing processes in FreeBSD, this chapter explains how to configure the kernel, device, and communications modes, create the spool directory, install printing filters, and enable printing in FreeBSD. The chapter also covers the administration of network printing functions, and it provides troubleshooting guidance for identifying and resolving a number of common printing problems.

The first part of this chapter assumes that you have a printer connected to a parallel port. It is possible to use FreeBSD with printers that connect to the serial port. However, serial printing is very slow, and is obsolete. Only ancient printers use serial printing. In addition, this chapter assumes that you know whether your printer understands PostScript. See your printer's documentation to find out.

> **NOTE**
> GDI printers, sometimes also called WinPrinters, don't work with FreeBSD at all. These printers are usually cheaper than non-GDI printers because they move some of the printer control off of the hardware and into a software driver. These printers have disadvantages: They use more system resources because the computer's CPU has to do much of the processing, rather than letting the printer do it, and they require special drivers that are usually available only for Windows. A very long list of operating systems simply will not work with these types of printers, and FreeBSD is one of them.

### IN THIS CHAPTER

- How `lp(8)`, the Print Spooler, and the Print Queue Function in FreeBSD
- Kernel, Device, and Communications Mode Configuration
- Creating the Spool Directory and Setting Its Permissions
- Setting Up Text and Conversion Filters
- Configuring `/etc/printcap` to Control Print System Functions
- Enabling `lp(1)` for Command-Line Printing
- Basic Command-Line Printing
- Printing from X-Windows
- Printing in StarOffice
- Using the `lpq(1)` Command to Check the Status of Print Jobs
- Removing Jobs from the Queue with the `lprm(1)` Command
- Controlling Printers
- Basic Network Printing
- Troubleshooting
