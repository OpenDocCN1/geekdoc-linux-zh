# DEBIAN GNU/LINUX 2.1

# Package format

Debian packages use a proprietary package format. (Before you start moaning – yet another package format! – you should consider that the Debian format developed prior to the RPM format. In its development of the RPM format, RedHat has assimilated many original ideas of Debian.)

# Topical

Sometimes the Debian distribution does not appear as up-to-date as other distributions. This is because each package (and each new version of a program) must first pass a beta test cycle before it is incorporated into the distribution. This quality control, however, also affects topicality. (Thus, Debian 2.1 is the only distribution described in this appendix still based on kernel version 2.0.)

# Updates

Usually, the Debian distribution can be updated during current operation by means of dselect.(In all other distributions, you need to restart your computer for an upgrade to a new version.)

Debian is a technically mature distribution – many other distributors could learn a lot from them – but it is very much when it comes to ease of operation. This applies in particular to the dselect package management program, however handling is to put it mildly – somewhat unconventional. The program is employed both for the first installation and for later system administration.

Insofar as packages are provided with configuration scripts, they are automatically started by dselect. Although in this way Debian can do without configuration tools, this configuration approach is far from error-proof. Another irritating factor is that the endless screen output during installation is not logged anywhere.

# Coral Linux

According to information circulating on the Internet, the envisaged Linux distribution of Corel Corporation will be based on Debian. For this distribution to be ready for the market, the installation in particular should be dramatically simplified.

# Internet

Further information on Debian philosophy, internal organization, mailing lists, bug reports., and other forms of quality assurance can be found on the Internet:

```
http://www.debian.org
ftp://ftp.debian.org
```

# Installation

> This section is based on Chapter 2, which gives general information on the installation of Linux, such as repartitioning the hard disk with FIPS or FDISK, creation of installation diskettes with RAWWRITE, and so on.