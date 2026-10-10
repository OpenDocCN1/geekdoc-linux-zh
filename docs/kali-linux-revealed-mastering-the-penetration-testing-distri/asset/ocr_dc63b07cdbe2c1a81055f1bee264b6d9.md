comes from Kali Linux (or is modified by Kali Linux). Any package that does not have kali in its version string (or in its package name) comes straight from Debian (Debian Testing in general).

| Double Check Before Filing Bugs against Debian | If you find a bug in a package imported straight from Debian, it should ideally be reported and fixed on the Debian side. However, before doing this, ensure that the problem is reproducible on a plain Debian system since Kali may have caused the problem by modifying other packages or dependencies.\n\nThe easiest way to accomplish this is to set up a virtual machine running Debian Testing. You can find an installation ISO for Debian Testing on the Debian Installer website:\n\n➥ https://www.debian.org/devel/debian-installer/\n\nIf you can confirm the problem in the virtual machine, then you can submit the bug to Debian by running reportbug within the virtual machine and following the instructions provided. |

Most bug reports about the behavior of applications should be directed to their upstream projects except when facing an integration problem: in that case, the bug is a mistake in the way the software gets packaged and integrated into Debian or Kali. For example, if an application offers compile-time options that the package does not enable or the application does not work because of a missing library (thus putting into light a missing dependency in the package meta-information), you may be facing an integration problem. When you don’t know what kind of problem you face, it is usually best to file the issue on both sides and to cross-reference them. Identifying the upstream project and finding where to file the bug report is usually easy. You just have to browse the upstream website, which is referenced in the Homepage field of the packaging meta-data:

```
```
$ dpkg -s sparta | grep "Homepage:
Homepage: https://github.com/SECFORCE/sparta
```
```

# 6.3.3. How to File a Bug Report

# *Filing a Bug Report in Kali*

Kali uses a web-based bug tracker at http://bugs.kali.org where you can consult all the bug reports anonymously, but if you would like to comment or file a new bug report, you will need to register an account.

# *Signing Up for a Bug Tracker Account*

To begin, simply click Signup for new account on the bug tracker website, as shown in Figure 6.1, “Kali Bug Tracker Start Page” [page 134].