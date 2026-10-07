# Using CVS GUI Clients

don't want to run the command in your home directory. Switch to a directory
where you will work on the files, and then run the checkout command.

```
cd -d /mnt/cvsroot/ checkout sample
```

Again, there's quite a bit going on here with the checkout line. The first part,
cvs, just starts CVS with the -d option specifying the cvsroot directory.
Finally, the checkout demodule section of the checkout command tells CVS to
check out the module sample. If successful, you will have several files placed
in the current directory that you can work with.

# Using CVS GUI Clients

For people who prefer not to memorize all the text-based commands for
CVS, there are multiple graphical CVS clients available. Some available
clients are Java-based, allowing the client to run on multiple OS platforms.
Setting up a Java environment is beyond the scope of this book, so we won't
cover that here. One popular CVS client for multiple platforms is TkCVS.

# Making CVS Simple with TkCVS

This section describes TkCVS, a GUI CVS client written in Tcl/Tk. The rea-
sason we chose this GUI client from other available clients is mostly that it's
simple to set up and with Tcl/Tk 8.1 or higher, TkCVS runs on Linux and other
UNIX-type OSes with Tcl/Tk 8.1 or higher, as well as Windows 9x or NT.

TkCVS does require Tcl/Tk version 8.1 or higher. Most Linux distributions
come with this already. If you're running a relatively recent version of Linux,
you should already have this installed.

# Installing TkCVS

TkCVS is particularly easy. You can download the latest version for
either Linux or Microsoft Windows from the TkCVS Web site at
http://www.twobarleycorns.net/tkcvs.html. You can also find the Linux ver
sion on the CD-ROM included with this book. The most recent version of
TkCVS is 6.4.