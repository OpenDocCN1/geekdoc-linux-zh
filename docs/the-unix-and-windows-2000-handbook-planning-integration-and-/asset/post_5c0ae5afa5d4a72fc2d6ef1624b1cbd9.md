
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

The master configuration file, sniglets.com.mc, must have an OSTYPE line. The locations of files and queues are controlled by this macro. The ostype directory contains a file for each supported operating system. Locate your operating system and change unknown to the applicable operating system (linux).

The OSTYPE line should be the first line after the VERSIONID line.

Previously, we created a sniglets.com.m4 file in the domain directory. To include the macros and features defined in this file, we need to add a DOMAIN line to our configuration file. This line should be placed after the OSTYPE line. Enter the following line in sniglets.com.mc:

```
DOMAIN(sniglets.com)
```

The final two lines specify the mailer type. The line MAILER(local) configures the local and prog MDAs. The local MDA delivers mail to users on the local machine. The prog MDA allows mail to be delivered by “piping” it through a program. This is not required if all of the mail is simply being relayed.

### Listing 9.2 Master Configuration File for sniglets.com

```
divert(-1)
#
# Copyright (c) 1998 Sendmail, Inc.  All rights reserved.
# Copyright (c) 1983 Eric P. Allman.  All rights reserved.
# Copyright (c) 1988, 1993
#     The Regents of the University of California.  All rights reserved.
#
# By using this file, you agree to the terms and conditions set
# forth in the LICENSE file which can be found at the top level of
# the sendmail distribution.
#
#
# This is the prototype file for a configuration that supports nothing
# but basic SMTP connections via TCP.
#
# You MUST change the 'OSTYPE' macro to specify the operating system
# on which this will run; this will set the location of various
# support files for your operating system environment.  You MAY
# create a domain file in ../domain and reference it by adding a
# 'DOMAIN' macro after the 'OSTYPE' macro.  I recommend that you
# first copy this to another file name so that new sendmail releases
# will not trash your changes.
#
divert(0)dnl
VERSIONID(`@(#)tcpproto.mc        8.10 (Berkeley) 5/19/1998')
OSTYPE(unknown)
MAILER(local)
MAILER(smtp)
```

The final line, MAILER(smtp), enables the Simple Mail Transfer Protocol (SMTP). This line activates SMTP, extended SMTP, SMTP8 (SMTP without converting 8-bit data to MIME), and the relay function. This line enables our Linux mail server to exchange mail with the rest of the Internet. This line assumes that all mailers are running DNS.
