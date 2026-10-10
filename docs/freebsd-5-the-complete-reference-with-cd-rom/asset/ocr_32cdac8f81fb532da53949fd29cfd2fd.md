299

# # Using Package Tools

The sysinstall package installation method can be convenient, but it’s not without its drawbacks. One of these is that you can install only packages that are available on a FreeBSD medium—typically a CD-ROM, DVD-ROM, or FTP site. (If you control a local FTP site or install from a hard disk, you can modify the INDEX file to add other packages, but doing so adds complexity that detracts from the convenience of sysinstall.)
Another problem with this method is that there’s little clue about the sizes of the packages you select. After you begin an installation, sysinstall provides information on data transfer rates for each package, but if your available disk space is limited, this information isn’t sufficient to judge whether you should try installing a potentially large package.

These problems are overcome by use of the underlying FreeBSD package tools. These programs reside in the /usr/sbin directory and have filenames that begin with pkg_. The most important of these is pkg_add, which adds a package to the system. In fact, sysinstall calls pkg_add to do its work, and if you watch the messages when you install a package, you’ll see a notice that it’s waiting for pkg_add at one point in the sysinstall package installation process.

> **Caution**
> Because pkg_add can add a package obtained from any source, it’s possible to use it to install a package that’s not trustworthy. You should pay attention to the advice in the upcoming section, “Verifying Software Authenticity,” before using pkg_add, especially on programs obtained from sources other than a FreeBSD CD-ROM, DVD-ROM, or FTP site.

The pkg_add syntax is

```
pkg_add [-vInfrRMS] [-t template] [-p prefix] package-name[...]
```

The meanings of the options to the command are

+   - **-v** This option enables verbose output, which may be useful for debugging purposes.

+   - **-I** Packages often include installation scripts that help customize a program for your system, and pkg_add normally runs such scripts. This option disables these scripts.

+   - **-n** This option causes pkg_add to report the steps it would take when installing a package, without actually performing the installation.

+   - **-f** Normally, pkg_add checks that a package’s dependencies are met before installing it. This option disables these checks. Normally, this is undesirable, but you might have reason to forego these checks; for instance, you might know that the dependencies are met by programs that were installed without using the package tools.