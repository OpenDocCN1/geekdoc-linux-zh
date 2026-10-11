# FIGURE 12.6

You use the pkgadd command to install the programs distributed as packages to your system.

![](bbox=[0.26, 0.14, 0.78, 0.55])

The pkgadd command makes a log entry every time it installs an application or utility. If you try to install a package that has already been installed, the utility will ask you if you want to install a previously installed package. If you answer yes, the pkgadd command will overwrite any and all of the files that are part of the installation.

The pkg rm (package remove) command returns a list of packages that are installed and can be removed. You will need to be a superuser to remove packages. For a new Ultra 5 workstation delivered from Sun with a standard SPARC Solaris 8 distribution, the pkg rm command returns a list of 1,003 files that were installed as packages. Figure 12.7 shows the routine used to remove the GNUtar program that was just installed. If you know the package that you want to remove, use the command pkg rm <packagename> directly.