will verify that the package ksh came in. If any of the tests fail, you will be closer to
understanding the source of the problems.

# # Managing Software with the YaST Command

The rpm command is a powerful but text-based tool and is the preferred, central software
installation manager for SuSE Linux. The YaST command (as shown in Figure 19.1) has a
graphical front end for Red Hat package management (using the rpm command), and is run
by root to install, update, or remove software on a SuSE Linux system. This command can
be run from the console or the command line of an X11 terminal window and offers local
and remote software management.

![](bbox=[0.068, 0.403, 0.69, 0.626])

When you use YaST to install software from a local computer, you must insert the SuSE
Linux CD-ROM (or CD-ROM number 1 if you use the commercial version of SuSE Linux)
in your computer before running the program. The yast command will automatically
mount the SuSE CD-ROM under the /var/admin/mount directory when it starts. You will not
be able to install software if the SuSE CD-ROM has been mounted on your filesystem,
even if it is mounted under the default /cdrom directory.

The yast command has a number of command-line options, but you can get a quick
summary by using the following:

+   * yast --help

The yast command's --mask option, followed by a specific keyword, can be used to jump
YaST directly to a specific function. For example, most SuSE administrators aiming to
install software will start the yast command with the following: