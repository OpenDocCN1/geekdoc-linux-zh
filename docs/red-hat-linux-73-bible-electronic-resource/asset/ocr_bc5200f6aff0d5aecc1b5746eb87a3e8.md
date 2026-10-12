# News server

Red Hat Linux comes with the Internet Network News Server (INN) software to let you set up a Red Hat Linux system as a news server. INN can provide your users access to thousands of Internet newsgroups.

By default, INN service is off in Red Hat Linux. To turn it on, change the kill script (`KO51nnd`) to a start-up script (`SO51nnd`). Do this by changing the files in the directories for run levels in which you want the service to run (probably `/etc/rc3.d` or `/etc/rc5.d`). For the service to be usable, you need to edit files in the `/etc/news` directory.

**CAUTION:** Because a news server can potentially consume huge amounts of system resources, you need to think carefully about how you configure it. See Chapter 22 for details about configuring your INN server.

# Print servers

The LPR New Generation (LPng) software is included as the default printer software for the current release of Red Hat Linux. As an alternative, the Common UNIX Printing System (CUPS) print server software is available for the first time in this release.

The LPng software is particularly well-suited for organizations in which a lot of people share many printers, such as on college campuses.

The LPng server (`lpd`) is started automatically when you boot your Red Hat Linux system (in run levels 2, 3, 4, or 5). However, unless you add one or more printers to the `/etc/printcap` file, no printers will actually be available for you to share. To add a printer manually, you must edit the `/etc/printcap.local` file. Also, any remote computer that you want to allow to access your computer must be added to the `/etc/lpd.perms` file. Global printing values (that is, ones that apply to all printers) can be added to the `/etc/lpd.conf` file.

**CROSS-REFERENCE:** Information on setting up printers can be found in Chapter 17.

The Common UNIX Printing System (CUPS) is a recently developed alternative to LPng and other printing interfaces that were built on facilities originally designed for line printers in the 1970s. CUPS is based on the Internet Printing Protocol (RFC 2616). Although it is compatible with other UNIX/Linux print facilities, CUPS is intended to make it easier to support new printers, protocols, and other devices as they become available.

The CUPS server (`cupsd`) is set up to run in run levels 2, 3, 4, and 5. However, because LPng is configured to be used as the printing service by default, you should run the `redhat-switch-printer` command if you want CUPS to be the default print service for your computer. Configuration files for CUPS are located in the `/etc/cups` directory.