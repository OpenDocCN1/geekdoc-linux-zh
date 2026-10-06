two files (the tarball and patch file; the .dsc file is optional) rather than just one. Debian source packages also support just one patch file, whereas source packages may contain multiple patch files. Although you can certainly combine multiple patch files into one, doing it less clear which patch comes from, making it harder to back out of any given change.

These source package differences are mostly of interest to software developers. As a system administrator or end user, you need not be concerned with them unless you recall a package from a source form—and even then, the differences between the formats are not overwhelming. The exact commands and features used by each system differ, but they accomplish overall goals.

Because all distributions that use Debian are derived from Debian, they tend to be more compatible with one another (in terms of their packages) than RPM-based distributions. In particular, Debian has defined its startup scripts and many features to help Debian packages install and run on any Debian-based system. This helps Debian-based systems avoid the sorts of incompatibilities in startup scripts that can cause problems using one distribution's RPMs on another distribution. Of course, some future distribution could violate Debian's guidelines for these matters, so this advantage isn't guaranteed to hold over time.

As a practical matter, it can be harder to locate Debian packages than RPM packages for some exotic programs. Debian maintains a good collection at http://www.debian.org/ and some authors make Debian packages available as well. If you can find an RPM but not a Debian package, you may be able to convert the RPM to Debian format using a program called *alien*, as described shortly in “Converting Between Package Formats.” If all else fails, you'll lose the advantages of the Debian package database.

# Configuring Debian Package Tools

With the exception of the APT sources list Debian package tools don't usually require configuration. Debian installs reasonable defaults (as its derivative distributions do). On occasions, you may want to adjust some of these defaults. Doing so requires you to know where to look for.

The main configuration file for *dpkg* is `/etc/dpkg/dpkg.cfg` or `~/.dpkg.cfg`. This file contains *dpkg* options, as summarized in Table 2.5, but without the dashing. For instance, to have *dpkg* always perform a test run before actually installing a package, you'd create a `dpkg.cfg` file that one line:

```
no-act
```

For APT, the main configuration file you're likely to modify is `/etc/apt/sources.list`, which was described earlier in “Using apt-get.” Another file is `/etc/apt/apt.conf`, which controls APT and dselect options. With *dpkg*, you won't need to modify *apt.conf*. If you need to make changes, the format is more complex and is modeled after those of the Internet Software Consortium's (ISC) Dynamic Host Configuration