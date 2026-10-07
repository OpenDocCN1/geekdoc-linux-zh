# A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

# Using slackpkg

slackpkg is the default utility for keeping Slackware up to date. It's extremely easy to configure and use. the man page provides clear instructions on using slackpkg with a good description of some of it's capabilities.

We start by picking a single "mirror" (Slackware repository) listed in the slackpkg configuration file. Open /etc/slackpkg/mirrors with vi (or your editor of choice). Uncomment a line and you're ready to go (delete the # sign from the front of an address). The line you un-comment needs to be for the specific architecture (32 bit vs 64 bit, etc.) and version of Slackware you are running.and should be near your geographic region (US, UK, Poland, etc.).

> Note that "Slackware-current" is a development branch of Slackware and is NOT suitable for our purposes. Do not select a mirror from the Slackware-current list.

The below example shows an edited /etc/slackpkg/mirrors file where a single mirror for a server in the USA has been un-commented (bold for emphasis - note the # has been removed). The mirror we are selecting for Slackware64-14.2. Select a mirror for your location.

```
root@forensic1#: vi /etc/slackpkg/mirrors
...
# Slackware64-14.2
#-
# USE MIRRORS.SLACKWARE.COM (DO NOT USE FTP - ONLY FINDS A NEARBY MIRROR)
http://mirrors.slack.com/slackware/slackware64-14.2/
# AUSTRALIA (AU)
# http://ftp.cc.swin.edu.au/slackware/slackware64-14.2/
# http://ftp.cc.swin.edu.au/slackware/slackware64-14.2/
# http://ftp.iinet.net.au/pub/slackware/slackware64-14.2/
# http://mirror.aernet.edu.au/pub/slackware/slackware64-14.2/
# http://mirror.aernet.edu.au/pub/slackware/slackware64-14.2/

```

One you may want to take with slackpkg to add several packages to the blacklist. The blacklist specifies those programs and packages that we do not want upgraded on a regular basis. We do this to avoid having to contemplate periodic security updates with changes to our bootloader and other components that add excessive complexity on the amass

> ^9Pay attention to the architecture and version. I made a mistake for when I was trying to upgrade Slackware64 (64 bit OS), not knowing I had selected a 32 bit mirror and therefore destroying my system when I updated.