```
/etc/ppp/options
/etc/ppp/pap-secrets
```

If you ever want to know which package a particular command or configuration file came from, you can use the `-qf` option. In the following example, the `-qf` option displays the fact that the chgrp command comes from the fileutils package:

```
# rpm -qf /bin/chgrp
coreutils-7.6-1.fc12.i386
```

Before you install a package, you can do the same queries on it that you would do on an installed package. This can be a great tool for finding information from a package while it is in your current directory, or even in a software repository. Here is an example of using the `-qp` option with `-i` to see the description of a package in a software repository:

```
# rpm -qp -i

http://ayo.freshrpms.net/fedora/linux/9/i386/freshrpms/RPMS/a52dec-0.7.4-8.fc7.i386.rpm
Name    : a52dec Relocations: (not relocatable)
Version : 0.7.4 Vendor: Freshrpms.net
Release : 8.fc7 Build Date: Wed 30 May 2007 01:02:28 PM CDT
Install Date: (not installed) Build Host: python3.freshrpms.net
Group   : Applications/Multimedia Source RPM: a52dec-0.7.4-8.fc7.src.rpm
Size    : 106856 License: GPL
Signature : DSA/SHA1, Wed 30 May 2007 01:02:58 PM CDT, Key ID 692ac55e42d5447b
Packager : Matthew Sauve <matthias@sauveforge.net>
URL     : http://liba52.sourceforge.net/
Summary : Library for decoding ATSC A/52 (aka AC-3) audio streams
Description :
liba52 is a free library for decoding ATSC A/52 streams. It is released under the terms of the GPL license. The A/52 standard is used in a variety of applications, including digital television and DVD. It is also known as AC-3.
```

In the previous example, the long command line shown on three lines should actually be typed on one line. If you are concerned about the content or legality of downloading a package, this example is a way to read the description of a package before you even download it.

In the following example, the command lists the files contained in a package that is in the current directory:

```
# rpm -qp -l AdobeReader\_enu-8.3.1-1.i486.rpm
```

Again, this is an excellent way to find out what is in a package before you install it.

# ### Verifying installed packages with rpm

If something in a software package isn’t working properly, or if you suspect that your system has been tampered with, the verify (-V) option of rpm can help you verify installed software against its original software package. Information about each installed package is stored on