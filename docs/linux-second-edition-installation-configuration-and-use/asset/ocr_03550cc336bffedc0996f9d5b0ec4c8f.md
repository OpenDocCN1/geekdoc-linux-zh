# REDHAT 6.0

to specify the sizes of the individual components because they overlap considerably.

If during component selection you activate the option SETUP INDIVIDUAL PACKAGES, you can subsequently activate or deactivate single packages of the various components. Generally, however, it makes sense to invest a lot of time in package selection during installation – once your installation has succeeded, you can always use the rpm or gnome tools for this purpose.

> Composition of the components is controlled by the file RedHat/base/comps on the installation CD-ROM. This text file contains a list of all packages that are installed per component. This file can be of valuable help if at a stage you want to install additional packages: gnome does not recognize components but displays all packages in a different hierarchy.

After selection of the required components and packages, these are installed into the previously created partitions. This process takes several minutes; progress is indicated with a bar diagram. (A log of all installed packages can be found after installation in /tmp/Install.log)

# Basic configuration

In many cases, the mouse is recognized automatically – you only need to confirm the selection. If your computer is connected to a local network, you can then proceed with the configuration of network card and network parameters. Even if you do not without, this basic TCP/IP functions are initialized to enable Linux programs to use this protocol for local communication. Then, your computer simply receives the name localhost.domain.

When configuring the time, you need to specify whether the CMOS clock of your computer is GMT (Greenwich Mean Time) or local time. Local time will probably be the. Furthermore, you need to specify the required time zone (for example Europe / Berlin). In the system configuration, you can simply confirm the default setting with [Enter].

Printer-set is of particular interest if you do not possess a PostScript printer. In this case, a file is created, which by means gs, converts PostScript files into the format of the relevant printer. This configuration step too can be carried out at a later time (using the printtool command under X).

Next, you are prompted to enter a password for root. In a further dialog you are asked whether you need NIS (common password management in a network), whether you want to use shadow passwords (which is more secure), and whether you to use MD5 passwords (this allows passwords of up to 256 characters length instead of the usual restriction to 8 characters). By default, NIS is deactivated, and shadow and MD5 passwords are activated; as a rule, you should simply accept this setting.

The question about creation of a boot diskette in any case will be answered with YES. Subsequently, you can install LILO either into the Master Boot Record (MBR) of your hard disk or into the root partition. And once more the all-important warning: never ever trust an installation program to install LILO into the MBR! Use