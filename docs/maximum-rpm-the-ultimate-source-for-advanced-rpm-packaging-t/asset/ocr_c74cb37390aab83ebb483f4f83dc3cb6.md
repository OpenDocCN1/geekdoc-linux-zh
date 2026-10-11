It's easy to see that if there were no `%files` list for the main package, and therefore, no main package, the tags in the main preamble would still be used in the source package. This is why RPM enforces the requirement that the main preamble contain copyright, `%description`, and group tags. So, here's a word to the wise: Don't put something stupid in the main preamble's `%description` just to satisfy RPM. Your witty saying will be immortalized for all time in every source package you distribute. (Yes, the author found out about this the hard way!)

# 18.6.1.1. Verifying Subpackage-Specific Install and Erase Scripts

The easiest way to verify that the %pre scripts we defined for each package were actually used is to simply install each package:

```
# rpm -Uvh foo-2.7-1.i386.rpm
foo    This is the foo package preinstall script
################################################

# rpm -Uvh foo-server-2.7-1.i386.rpm
foo-server    This is the foo-server subpackage preinstall script
################################################

# rpm -Uvh foo-client-2.7-1.i386.rpm
foo-client    This is the foo-client subpackage preinstall script
################################################

# rpm -Uvh bazlib-5.6-1.i386.rpm
bazlib    This is the bazlib subpackage preinstall script
################################################
#
```

As expected, the unique %pre script for each package has been included. Of course, if we hadn't wanted to actually install the packages, we could have used RPM's `--scripts` option to display the scripts:

```
# rpm -qp --scripts foo-2.7-1.i386.rpm
preinstall script:
echo "This is the foo-server subpackage preinstall script"

postinstall script:
(none)
preuninstall script:
(none)
postuninstall script:
(none)
verify script:
(none)
#
```

This approach might be a bit safer, particularly if installing the newly built package would disrupt operations on your build system.