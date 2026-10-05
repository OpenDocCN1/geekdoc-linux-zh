+   server standard with FTP, WWW, DNS, NIS, POP, no X (50 Mbytes)

+   server complete, plus maillist, backup, nems, samba, squid (70 Mbytes)

The optimal choice is not easy; the more packages you install, the more configuration you need to answer (instantly). 'Standard without X' is quite attractive – in this way you obtain a running system relatively quickly, and just need to install any additional packages you require manually at a later stage (This obviously requires a fairly advanced knowledge of Linux – but without this knowledge, you would despise Debian anyway.) After the selection of the required profile, dselect is started automatically.

# dselect during first installation

This section briefly describes the steps needed to conclude the installation. It is followed by more detailed information on the handling of the program (for example, for later installation of a specific package).

Essentially, you need to execute the three commands ACCESS, UPDATE, and INSTALL with INSTALL probably having to be repeated several times (each with a change of CD-ROM).

In several variations to access the installation data are available. If the data is found on one or more CD-ROMs, you should select multi.

To make the installation program really find all required packages, it is mandatory that the last binary CD is currently present in the CD-ROM where you select multi.

Usually, a Debian 2.i distribution consists of four CDs. CDs 1 and 2 contain the binary packages, while CDs 3 and 4 contain the source code. In this case, CD 2 must be present in the drive. (This also applies if you have a fifth contrib CD. During a first installation, its contents play no role.)

Subsequently, you need to specify the name of your CD-ROM drive. As a rule, you can simply accept the default /dev/cdrom. This is a link to the actual device; this link has already been created during the earlier installation steps.

Now dselect tries to find the paths to the packages. The main and contrib packages are recognized automatically. The non-free, non-US, and local packages however, are mostly for for vain – they are usually not included on the installation CDs. Just indicate 'none'.

The next command is UPDATE. With this, dselect reads the list of available packages (which takes only a few seconds).

Finally, INSTALL starts the installation as such. It will promptly come up with an error message – dselect does not find an essential package on CD 2 and asks you to insert CD 1. Subsequently, you execute INSTALL. An endless list of screen output follows in which dselect reports on which packages is installing. From time to time, you are prompted for configuration specifications of packages. If you feel overstressed with this, you can nearly carry out the configuration at a later stage or simply accept the proposed default settings with next. An overview of