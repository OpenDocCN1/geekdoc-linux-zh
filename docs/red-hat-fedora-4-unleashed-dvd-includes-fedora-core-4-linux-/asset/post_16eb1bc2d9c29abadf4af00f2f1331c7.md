
## Two Handy Options

By appending `vh` to any option, you get:
- `v`: Some status feedback.
- `h`: Hash marks as the work proceeds.

Many additional options can also be added to or used in conjunction with these options. These are summarized in the following table:

| **Option** | **Used To** |
|---|---|
| `rpm -i` | Install a package |
| | Useful options to `-i`: |
| | `--excludedocs`: Does not install documentation to save space. |
| | `--replacepkgs`: Replaces the package with a new copy of itself. |
| | `--force`: The "big hammer"—Ignores all warnings and installs anyway. |
| | `--noscripts`: Does not execute any pre- or post-install scripts. |
| | `--nodeps`: Ignores any dependencies. |
| | `--root path`: Sets an alternative root to path. |
| `rpm -e` | Erases (deletes) a package. |
| | Useful option to `-e`: |
| | `--nodeps`: Ignores any dependencies. |
| `rpm -U` | Upgrades a package, removing the older one but keeping modified files, such as configurations. |
| | Useful options to `-U`: |
| | `--oldpackage`: Permits downgrading to an older version. |
| | Other options are the same as with `rpm -i`. |
| `rpm -q` | Queries about package information |
| | Useful options to `-q`: |
| | `-p file`: Displays all information about the package file. |
| | `-f file`: What package owns the file file? |
| | `--whatprovides x`: Determines what packages provide x. |
| | `--whatrequires x`: Determines what packages require x. |
| | `-i`: Summarizes the package information. |
| | `-l`: Lists the files in package. |
| | `--scripts`: Displays the contents of any install, uninstall, or verifies scripts. |
| | `--provides`: Displays the capabilities package provides. |
| | `--requires`: Displays the capabilities package requires. |
| `rpm -V` | Verifies packages against the RPM database |
| | Useful options to `-V`: |
| | `-a`: Verifies all installed packages. |
| `rpm -K` | Uses GPG to verify a downloaded package. |
| | Useful options to `-K`: |
| | `--nosignature`: If you lack public GPG encryption keys, do not have GPG installed, or are legally prohibited from using GPG, this still verifies the package using size and MD5 checksums. |

Details on obtaining the Fedora Core public GPG encryption key and using it are at http://www.rpm.org/max-rpm/s1-rpm-checksig-using-rpm-k.html.

![](img/774d40fd20903495c5cd00e2efad3f33_226_0.png)

### Using `rpm` on the Command Line

Because the new graphical RPM client can only install and uninstall RPM packages (for now—more functionality is promised), you will still end up administering RPM packages from the command line. You can perform all the five basic `rpm` operations using the `rpm` command from the command line. This section gives you an introduction to performing those operations. It also provides examples of how to install, verify, query, remove, and upgrade a software package.

The most common `rpm` operation is software installation. Using `rpm` is an easy way to keep track of installed software, and it can be used to quickly remove undesired packages. Use the `-i` option, along with the full or partial name (using regular expressions) of a software package, to install software with `rpm`. For example, to install the `unace` archiving package, use the `rpm` command like this:

```bash
# rpm -ivh http://mirrors.zoreil.com/p1.f.zarb.org/mandrake/10.0/i586/unace-2.2-2plf.i586.rpm
Retrieving http://mirrors.zoreil.com/p1.f.zarb.org/mandrake/10.0/i586/unace-2.2-2plf.i586.rpm
warning: /var/tmp/rpm-xfer.48amVs: V3 DSA signature: NOKEY, key ID 8df56d05
Preparing...                                    ########################################### [100%]
   1:unace
########################################### [100%]
```

This example uses the `v` and `h` options, which provide a more verbose output and display of hash marks to show the progress of the installation. The example also demonstrates the capability of `rpm` to use HTTP or FTP servers to fetch files for installation. It also shows that `rpm` can use GPG keys to validate a file. (The key was not installed in our example.)

You can also use `rpm` to query its database after installing packages to verify an installation. Use the `-V` option, along with the name of a software package, to verify installation of your system. For example, to verify the `unace` archiving package, use the `rpm` command like this:

```bash
# rpm -V unace
```

> **NOTE**
> If everything is correct with your software installation, your system will display no response to `rpm -V` after you run the command; only problems are displayed.

As you can see from the following program output, you can get additional information about a package by adding additional verification options (such as two more `v`'s) to the `-v` option. To get more information about an installed package, use one or more forms of the `rpm` query options. For example, to display concise information about an installed package, use the `-q` option, along with the `i` option and the installed package name, like this (note that your version will be different from that shown here):

```bash
# rpm -qi unace
Name          : unace                             Relocations: (not relocatable)
Version       : 2.2                               Vendor: Penguin Liberation Front
Release       : 2plf                              Build Date: Sat 01 Mar 2003 12:13:48 PM EST
Install date: Tue 02 Sep 2003 03:46:28 PM EDT     Build Host: badger.subversion.alt
Group         : Archiving/Compression              Source RPM: unace-2.2-2plf.src.rpm
Size          : 401368                            License: freeware
Packager      : Guillaume Rousse <guillomovitch@zarb.org>
URL           : http://www.winace.com
Summary       : Decompressor for .ace format archives
Description   :
Unace is a utility to extract, view, and test the contents of an ACE archive.
```

This form of the `rpm` query provides quite a bit of information about the software package. (You can also query packages before installation by providing a pathname for them.)

If this package is not up-to-date, you can easily and quickly upgrade the package by downloading a newer version and then using `rpm`'s `-U` or upgrade option like this:

```bash
# rpm -Uvh unace-2.2-2plf.i386.rpm
Preparing...                     ######################################## [100%]
  1:unace                       ######################################## [100%]
```

Note that it wasn't necessary to remove the currently installed software package—the `U` option removes the old version of the software (saving the old configuration files), and then automatically installs the new software.

You can also upgrade your system software by using the `rpm` command's `-F` or “freshen” option, which will fetch a designated package from a remote FTP or HTTP server. For example, to upgrade the `fetchmail-conf` package, use `rpm` like this:

```bash
# rpm -Fv ftp://ftp.tux.org/linux/redhat/updates/9/en/os/i386/initscripts-7.14-1.i386.rpm
Retrieving ftp://ftp.tux.org/linux/redhat/updates/9/en/os/i386/initscripts-7.14-1.i386.rpm
Preparing packages for installation...
initscripts-7.14-1
```

Use the `-e` option, along with the name of a software package, to remove or erase software from your system with `rpm`. For example, to remove the `unace` archiving package, use the `rpm` command like this:

```bash
# rpm -e unace
```

Note that if the operation succeeds, no messages will be displayed on your system. You can quickly search for the names of installed packages by piping the output of `rpm -qa` through the `grep` and `sort` commands (see Chapter 5, “First Steps with Fedora,” for additional information on `grep` and `sort`); here's how to do that search:

```bash
# rpm -qa | grep mail | sort
fetchmail-6.2.0-7
mailcap-2.1.14-1.1
mailx-8.1.1-31.1
mozilla-mail-1.4.1-8
procmail-3.22-11
sendmail-8.12.10-1.1
sendmail-cf-8.12.10-1.1
```

This example returns a sorted list of all packages with names containing the word `mail`.

> **NOTE**
> Another essential feature of the `rpm` command is its `--rebuilddb` option. If your system's RPM database becomes corrupted, this is your first (and perhaps only) option for restoring software management services. We hope that you never have to use this option; help ensure that by always backing up your data!
