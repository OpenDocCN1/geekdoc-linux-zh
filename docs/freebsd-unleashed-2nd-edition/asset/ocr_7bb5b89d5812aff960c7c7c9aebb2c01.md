> **TIP**
> Not all software available for FreeBSD is available as a package. Sometimes it's too new; some- times it's too rapidly developing. Whatever the reason, you won't get the complete list of ported software by reading the package listings. The complete set of software you can install is found in an up-to-date ports collection, discussed later in this chapter.

As you learned in Chapter 10, some programs need to be configured before they can be used. Go into /usr/local/etc and check for a config file (usually of the style <program_name>.conf or <program_name>.cfg, or at least containing the program name). If the file has .sample at the end, you need to perform some additional configurations and remove the .sample part before the program can use it. Open the file with your favorite text editor and do what needs to be done, as described in comments in the file itself or in the man page for the program. After you have configured the first file, check inside the rc.d subdirectory for similar files and deal with them in the same way.

# Using pkg_add

Few options are available for the actual installation process in FreeBSD. Because executables, config files, and libraries are all kept in a standard centralized location, no dialog asks where you want to install a program or offers you any of the custom installation options you get in the desktop OS world. These installation limitations are perfect examples of both the more “closed-box” approach of FreeBSD, as compared to that of Linux, and the centralized distribution model for all the open-source software available for the platform.

However, there are times when you need more control over a package than you can get within sysinstall. Examples include packages that have interactive preinstallation scripts (in which you can set options specific to that package) and situations in which the automated installation in sysinstall fails. For times such as these, you need the pkg_add tool; it's used in every package installation, whether it's called directly or run by sysinstall.

The pkg_add tool is designed to operate on a .tgz file you've already downloaded (from the per-release distribution directory described earlier) or on a remote file specified by its URL. For instance, the following two procedures are roughly equivalent:

```
```
# fetch ftp://ftp.FreeBSD.org/pub/FreeBSD/releases/i386/4.6.2-RELEASE/
packages/www/roxen-2.1.231.tgz
# pkg_add roxen-2.1.231.tgz
```
```

and

```
```
# pkg_add ftp://ftp.FreeBSD.org/pub/FreeBSD/releases/i386/4.6.2-RELEASE/
packages/www/roxen-2.1.231.tgz
```
```