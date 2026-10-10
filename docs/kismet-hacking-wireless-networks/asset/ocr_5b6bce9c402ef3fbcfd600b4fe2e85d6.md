configuration. There are a huge amount of options here to configure, way more than we need to worry about. All that matters is the target system. This is where you can specify the architecture you are building for. The target system setting for the WRT54GL is “Broadcom BCM947xx/953xx,” and the most stable is the 2.4 kernel. For the purposes of this section, we are not going to change anything else except to build Kismet through the buildroot.

The existing Kismet in the buildroot can be enabled in the menuconfig under network \ | wireless. Select the Kismet modules you want to build (you can build the server, client, and drone) and make sure they are selected as modules (it should say *<M>* beside the name). This builds them as packages rather than into the base openwrt image.

Go back to the main screen and exit, then save the config and you are returned to the command line. If you type “make” at this point, you will download the sources for everything selected, build the base system, base libraries, and any libraries needed by Kismet, as well as the Kismet binaries. Now, if you want to upgrade the version of Kismet that the buildroot builds, you need to edit the Makefile the buildroot uses, and change where it gets its sources from and adjust a few build options.

Within the buildroot, the packages are built according to a Makefile that contains the location of the source code, the build options, and a list of dependencies. We need to edit this file to use the newer source, as well as make some adjustments to version numbers.

The Kismet package Makefile is located in the buildroot directory under *packages/feeds/packages/kismet*. The existing Makefile should look something like this:

```
#
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id$
include $(TOPDIR)/rules.mk
PKG_NAME:=kismet
PKG_VERSION:=2007-10-R1
PKG_RELEASE:=1
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.kismetwireless.net/code
PKG_MD5SUM:=2100c667e9cb0d0ce3fa2d0c851e2
```