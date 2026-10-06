# Querying and Verifying Package Contents 299

SysVinit 172531
xVMware 10788833
X11R6-contrib 458224
XFree86 14611173
XFree86-100dpi-fonts 1258246

etc. The syntax of the --queryformat argues rather that the C printf library function. If you are unfamiliar with C, the syntax rather daunting, but you probably won't have to work with it on the RHCE exam. To learn the tags that correspond to RPM database items, issue the com-

```
rpm --querytags
```

A particularly useful query lists packages and the capabilities provide. You can use such a query to learn, for example, what package provides the librpm.so.0 library.

```
# rpm -qp --queryformat "%16{NAME}\t%10{PROVIDES}\n"
►.rpm | \grep librpm.so.0
librpm.so.0
```

The single line of output shows that the rpm package provides the librpm.so.0 library, just as one might expect.
 Hat Linux 6.2 and later include the rpmdb-redhat package that contains an alternate RPM database describing the contents of the release. If you install this package, you can use the rpm command special-
redhatprovides flag to determine what package owns a particular file. This capability is helpful in resolving dependencies. For example, suppose you try to install a package but receive an error message stating that a particular library is required—say, libsample.so.1. The following command identifies the package containing the missing library:

```
rpm -q --redhatprovides libsample.so.1
```