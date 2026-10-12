
Another way of getting verification that the install is actually working is to add the `-h` option, as in the following example:

```
# rpm -ivh audiofile-devel-0.2.1-2.i386.rpm
audiofile-devel ###################################################
```

With the `-h` option, rpm chugs out 50 hash marks (#) until the package is done installing. As you can see, when everything goes well, installing with rpm is quite simple. Some problems can occur, however. Here are a couple of them:

- **Package dependencies errors** — If the package you are installing requires an additional package for it to work properly, you will see an error noting the missing package. You should get and install that package before trying your package again. (You can override the failure with install options described above, but I don’t recommend that because your package may not work without the dependent package.)
- **Nonroot user errors** — If rpm `-i` is run by someone who is not the root user, the command will fail. The output will indicate that the `/var/lib/rpm` database could not be opened. Log in as root user and try again.

## Upgrading packages with rpm

The upgrade option (-U) with rpm behaves pretty much like the install option. The difference is that it uninstalls the old package before installing the new version of the package. The format is:

```
# rpm -U [options] package
```

> **TIP:** You can use the `-U` option regardless of whether you are doing a new install or an upgrade. With `-U`, the package will install in either case. So rpm `-U` will always work, while rpm `-i` will fail if the package is already installed.

One issue when upgrading is installing an older version of a package. For example, if you install a new version of some software and it doesn’t work as well, you will want to go back to the old version. To do this, you can use the `--oldpackage` option as follows:

```
# rpm -U --oldpackage AnotherLevel-0.7.4-1.noarch.rpm
```

If a later package of this name already exists, it is removed and the older version is installed.

## Removing packages with rpm

If you no longer want to use a package (or you just want to recover some disk space), use the `-e` option to remove a package. In its simplest form, you use rpm with the `-e` option as follows:

```
# rpm -e package
```

If there are no dependencies on this package, it is silently removed. Before you remove a package, however, you may want to do a quick check for dependencies. The `-q` option is used for a variety of query options. (Checking for dependencies isn’t necessary because rpm checks for dependencies before it removes a package. You may want to do this for your own information, however.) To check for dependencies, do the following:

```
# rpm -q --whatrequires package
```

If you decide to remove the package, I recommend using the `-vv` option with `rpm -e`. This lets you see the actual files that are being removed. I also suggest that you either direct the output to a file or pipe it to `more` because the output will probably run off the screen. Here’s an example:

```
# rpm -evv xpi | more
```

This example removes the `xpi` package and shows you the files that are being removed one page at a time. (Press the Spacebar to page through the output.)

Other options that you can run with `rpm -e` can be used to override conditions that would prevent the package from being removed or to prevent some processing (such as not running preuninstall and postuninstall scripts). Three of those options are as follows:

- `--nodeps` — Uninstall the package without checking for dependencies.
- `--noscripts` — Uninstall the package without running any preuninstall or postuninstall scripts.
- `--notriggers` — Uninstall the package without executing scripts that are triggered by removing the package.

If you feel nervous about **boldly** removing a package, you can always run the uninstall in test mode (`--test`) before you do the real uninstall. Test mode shows you everything that would happen in the uninstall without actually uninstalling. (Add the `--vv` option to see the details.) Here’s an example:

```
# rpm -evv --test xpi | more
D: counting packages to uninstall
D: opening database in /var/lib/rpm/
D: found 1 packages to uninstall
D: uninstalling record number 4545368
D: will remove files test = 1
D: /usr/share/doc/xpi-4.3.2-1/doc/man/xpis.man.msub - removing
D: /usr/share/doc/xpi-4.3.2-1/doc/man/xpis.man - removing
.
.
.
D: /etc/X11/wmconfig/xpi - removing
D: removing database entry
```

If the results look fine, you can run the command again, without the `--test` option, to have the package removed.

## Querying packages with rpm

Using the query options (`-q`) of `rpm`, you can get information about RPM packages. This can be simply listing the packages that are installed or printing detailed information about a package. Here is the basic format of an `rpm` query command (at least one option is required):

```
# rpm -q [options]
```

The following are some useful options you can use with an `rpm` query:

- `-qa` — Lists all installed packages.
- `-qf file` — Lists the package that owns `file`. (The file must include the full path name or `rpm` assumes the current directory.)
- `-qi package` — Lists lots of information about a `package`.
- `-qR package` — Lists components (such as libraries and commands) that `package` depends on.
- `-ql package` — Lists all the files contained in `package`.
- `-qd package` — Lists all documentation files that come in `package`.
- `-qc package` — Lists all configuration files that come in `package`.

To list all the packages installed on your computer, use the `-a` query option. Because this is a long list, you should either pipe the output to `more` or, possibly, use `grep` to find the package you want. The following command line displays a list of all installed RPM packages, and then shows only those names that include the string of characters `xfree`. (The `-i` option to `grep` says to ignore case.)

```
# rpm -qa | grep -i xfree
```

If you are interested in details about a particular package, you can use the `rpm -qi` query option. In the following example, information about the `dosfstools` package (for working with DOS filesystems in Linux) is displayed:

```
# rpm -qi dosfstools
Name        : dosfstools    Relocations: (not relocatable)
Version     : 2.8           Vendor: Red Hat, Inc.
Release     : 1            Build Date: Fri 06 Jul 2001 08:29:15 AM PDT
Install date: Fri 05 Apr 2002 12:42:28 PM PDT  Build Host: redhat.com
Group       : Applications/System  Source RPM: dosfstools-2.8-1.src.rpm
Size        : 67734         License: GPL
Packager    : Red Hat, Inc. <bugzilla.redhat.com/bugzilla>
Summary     : Utilities to make/check MS-DOS FAT filesystems on Linux.
Description :
```

The `dosfstools` package includes the `mkdosfs` and `dosfsck` utilities, which respectively make and check MS-DOS FAT filesystems on hard drives or on floppies.

To find out more about a package’s contents, you can use the `-l` (list) option with your query. The following example shows the complete path names of files contained in the `xpiilot` package:

```
# rpm -ql xpiilot | more
/etc/X11/wmconfig/xpiilot
/etc/X11/wmconfig/xpiilots
/usr/X11R6/bin/xp-replay
/usr/X11R6/bin/xpiilot
...
```

Would you like to know how to use the components in a package? Using the `-d` option with a query will display the documentation (man pages, README files, HOWTOs, and so on) that is included with the package. If you are having trouble getting your X Window System running properly, you can use the following command line to find documents that may help:

```
# rpm -qd XF8686 | more
/usr/X11R6/man/man1/editres.1x.gz
/usr/X11R6/man/man1/iceauth.1x.gz
/usr/X11R6/man/man1/lbxproxy.1x.gz
/usr/X11R6/man/man1/libxrx.1x.gz
/usr/X11R6/man/man1/lsdir.1x.gz
/usr/X11R6/man/man1/makedepend.1x.gz
/usr/X11R6/man/man1/makespres.1x.gz
/usr/X11R6/man/man1/makesstrs.1x.gz
/usr/X11R6/man/man1/mkcfm.1x.gz
...
```

Many packages have configuration files associated with them. To see what configuration files are associated with a particular package, use the `-c` option with a query. For example, this is what you would type to see configuration files that are used with the `ppp` package:

```
# rpm -qc ppp
/etc/pam.d/ppp
/etc/ppp/chap-secrets
/etc/ppp/options
/etc/ppp/pap-secrets
```

If you ever want to know which package a particular command or configuration file came from, you can use the `-qf` option. In the following example, the `-qf` option displays the fact that the `chgrp` command comes from the `fileutils` package:
