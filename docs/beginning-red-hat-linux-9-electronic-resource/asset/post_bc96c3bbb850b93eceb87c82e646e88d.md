
The syntax for a basic query is as follows:

```
rpm -q [options] <filename>
```

## Try It Out: Querying RPM for Information about a Package

- 1. Open a terminal window (by selecting **Main Menu | System Tools | Terminal**).

- 2. RPM package operation can be performed only by a user with root privileges. So, if you're not logged in as root, do so now, by using the `su` command:

```text
$ su -
Password:
```

- 3. Change to the packages directory of CD 2 in your Red Hat by inserting the CD and typing the following, once it has mounted:

```text
# cd /mnt/cdrom/RedHat/RPMS/
```

- 4. Now, let's find the information for the `lynx` package (Lynx is a text-based browser). To do this, type the following at the command line:

```text
# rpm -qip lynx-2.8.5-11.i386.rpm
```

Here, `-qip` represents the command options (which we'll discuss in more detail shortly), and `lynx-2.8.5-11.i386.rpm` is the RPM package file we're interested in. After a short while, you should see the following response:

```text
Warning: lynx-2.8.5-11.i386.rpm: V3 DSA signature: NOKEY, key ID db42a60e
Name   : lynx                    Relocations: (not relocatable)
Version  : 2.8.5                   Vendor: Red Hat, Inc.
Release  : 11                      Build Date: Sat 25 Jan 2003 05:10:43 GMT
Install Date: Thu 15 May 2003 11:41:58 BST   Build Host: porky.devel.redhat.com
Group  : Applications/Internet   Source RPM: lynx-2.8.5-11.src.rpm
Size   : 4021040                 License: GPL
Signature : DSA/SHA1, Mon 24 Feb 2003 06:34:45 GMT, Key ID 219180cddb42a60e
Packager : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
URL    : http://lynx.isc.org/
Summary  : A text-based Web browser.
Description :
Lynx is a text-based Web browser. Lynx does not display any images,
but it does support frames, tables, and most other HTML tags. One
advantage Lynx has over graphical browsers is speed; Lynx starts and
exits quickly and swiftly displays webpages.
```

*Notice the warning in the first line? We'll explain it later in the chapter, when we cover verification.*

Useful, isn't it? You can use this information to make sure you're installing what you think you're installing and to check that you've got the right version of software.

- 5. RPM can also be used to query a specific package installed on the system. Issue the following command as root:

```text
rpm -qi lynx
```

Here, *-qi* represents the command options, and *lynx* is the RPM package file name we're interested in. After a short while, you should see the following response:

```text
Name       : lynx
Version    : 2.8.5
Release    : 11
Install Date: Mon 26 May 2003 14:50:02 BST
Group      : Applications/Internet
Size       : 4021040
Signature  : DSA/SHA1, Mon 24 Feb 2003 06:34:45 GMT, Key ID 219180cddb42a60e
Packager   : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
URL        : http://lynx.isc.org/
Summary    : A text-based Web browser.
Description:
Lynx is a text-based Web browser. Lynx does not display any images,
but it does support frames, tables, and most other HTML tags. One
advantage Lynx has over graphical browsers is speed; Lynx starts and
exits quickly and swiftly displays webpages.
Relocations: (not relocatable)
Vendor: Red Hat, Inc.
Build Date: Sat 25 Jan 2003 05:10:43 GMT
Build Host: porky.devel.redhat.com
Source RPM: lynx-2.8.5-11.src.rpm
License: GPL
```

- 6. Now let's try something a little different, but no less useful. Issue the following command (still as root):

```text
# rpm -qa
```

This command makes a query for all the packages that are installed on your system; you should get something like this in response:

```text
rpmi04-python-4.0.4-8x.27
ksymoops-2.4.5-1
libgail9-0.19.2-4
setup-2.5.25-1
...gnome-media-2.2.1.1-4
redhat-switch-printer-0.5.16-1
sharutils-4.2.1-14
vnc-server-3.3.3r2-47
```

- 7. Here’s another example. You are likely to encounter situations in which you need to know about the package that owns a particular command on the system. For example, let’s find out which package owns the command `/usr/bin/lynx`. To do this, type the following at the command line:

```text
# rpm -qf /usr/bin/lynx
```

You should get the following response:

```text
lynx-2.8.5-11
```

Thus, it is the lynx-2.8.5-11 package that is used by the system, whenever a user calls the command `/usr/bin/lynx`.

- 8. Finally, RPM also provides a command that allows us to find out the list of all files contained in an RPM package. Let’s find out what files are contained in a samba-client package… To do this, type the following:

```text
# rpm -ql lynx
```

Here’s the response you should get:

```text
/etc/lynx-site.cfg
/etc/lynx.cfg
/etc/lynx.cfg.cs
/etc/lynx.cfg.ja
/etc/lynx.cfg.sk
/usr/bin/lynx
......
/usr/share/locale/sl/LC_MESSAGES/lynx.mo
/usr/share/locale/sv/LC_MESSAGES/lynx.mo
/usr/share/man/man1/lynx.1.gz
```

## How It Works

When we query an RPM package file using RPM command line options, it displays the information like name, version, release, group, summary and description of the package. The exact type of the query and the format of the resulting output depend on the command options that we specify:

- In all five of the queries in the example above, we used -q. The q is to indicate that we’re making a query.
- In the step 4 and 5, we used -qip. The p indicates that we are querying a package, and the i indicates that we want to see the package information.
- In Step 6, we used -qa. The a indicates that we are querying *all* currently-installed packages.
- In Step 7, we used -qf. The f indicates that we wish to query the package that owns the specified file.
- Finally, in Step 8, we used -ql. The l indicates that we wish to query the list of files contained in the specified package.

## RPM Package Security

RPM has had a number of releases over the years, and the latest versions (one of which is bundled with your system) have a few new features. One new feature of interest to us is that RPM now checks the **signature** of a package when querying, installing, or upgrading it.

Checking the signature of a package allows you to ensure that it is from a trustworthy source. All official Red Hat Packages are signed by Red Hat using its GnuPG key, and RPM checks the package's GnuPG signature against the Red Hat GnuPG key to make sure the package is what it claims to be. If you do not have an appropriate key installed to verify the signature, then you will get a warning message like this (we mentioned it earlier, remember?):

```text
warning: lynx-2.8.5-11.i386.rpm: V3 DSA signature: NOKEY, key ID db42a60e
```

The exact content of the warning message depends on the situation. For example, if RPM cannot verify the GnuPG signature of the package then you will see the following error message:

```text
error: V3 DSA signature: BAD, key ID 0352860f
```

By contrast, if RPM cannot find the appropriate key to verify the signature of a package, you will get this warning:

```text
warning: V3 DSA signature: NOKEY, key ID 0352860f
```

GnuPG signatures are digital signatures that are very hard to forge. Signatures are created with a unique secret key and can be verified by their recipient using a public key. A digital signature timestamps a document so that if anyone tries to tamper or modify it, the verification of the signature will fail.

### Red Hat GNU Privacy Guard (GPG) Keys

To install Red Hat's GPG keys on your installed system, issue the following command:

```text
# rpm --import /usr/share/rhn/RPM-GPG-KEY
```

or, use the following, to install them from CD-ROM (make sure you've got the right one in the drive):

```text
# rpm --import /mnt/cdrom/RPM-GPG-KEY
```

These commands will install Red Hat's public GPG keys onto your system. You can also import other vendors' GnuPG keys in much the same way; just change the name of the file to the one that they've supplied to you.

To display a list of all GnuPG keys installed for RPM package verification on your system, issue the following command:

```text
# rpm -qa gpg-pubkey*
gpg-pubkey-db42a60e-37ea5438
```

This will return a list of results. If you've installed the Red Hat key, you should see the following listed amongst them:

```text
gpg-pubkey-db42a60e-37ea5438
```

We can get even more complete details of a Red Hat GPG key by executing the following command:

```text
# rpm -qi gpg-pubkey-db42a60e-37ea5438
```

In the above command, note that `gpg-pubkey-db42a60e-37ea5438` is the name of the Red Hat GnuPG key, gathered from the output of the command `rpm -qa gpg-pubkey*`.
