```
# Copyright (c) 1998 Sendmail, Inc. All rights reserved.
# Copyright (c) 1983 Eric P. Allman. All rights reserved.
# Copyright (c) 1988, 1993
#
# The Regents of the University of California. All rights reserved.
#
#
# By using this file, you agree to the terms and conditions set
# forth in the LICENSE file which can be found at the top level of
# the sendmail distribution.
#
#
#
# The following is a generic domain file. You should be able to
# use it anywhere. If you want to customize it, copy it to a file
# named with your domain and make the edits; then, copy the appropriate
# .mc files and change `DOMAIN(generic)' to reference your updated domain
# files.
#
divert(0)
VERSIONID(`@(#)generic.m4	8.9 (Berkeley) 5/19/1998')
define(`confFORWARD_PATH',
`$:/.forward.$w:$:/.forward.$h:$:/.forward.$w:$:/.forward')dnl
FEATURE(redirect)dnl
FEATURE(use_cw_file)dnl
```

The master configuration file for sendmail.cf is located in the cf directory (cf/cf). This directory contains generic text configuration files named according to the type of UNIX version you have (e.g., generic-hpux10.mc, generic-solaris2.mc, etc.). Try to select a generic file that most closely matches your workstation/server. Make a copy of this file and give it your domain name.

We will configure a Linux workstation to be the main mail server for sniglets.com. The tcpproto.mc file is selected to serve as a template for developing our configuration file. Make a copy of the tcpproto.mc file, but change the name to your domain (sniglets.com.mc, Listing 9.2).

The master configuration file, sniglets.com.mc, must have an OS-TYPE line. The locations of files and queues are controlled by this macro. The ostype directory contains a file for each supported operating system. Locate your operating system and change unknown to the applicable operating system (linux).

The OSTYPE line should be the first line after the VERSIONID line.

Previously, we created a sniglets.com.m4 file in the domain directory. To include the macros and features defined in this file, we need to add a DOMAIN line to our configuration file. This line should be placed after the OSTYPE line. Enter the following line in sniglets.com.mc: