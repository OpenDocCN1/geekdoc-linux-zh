# Example 4.1: RPM Spec File for Widgets

```
#
# RPM Package Manager (RPM) spec file for Widgets :-)
#
Summary: Some generic program
Name: widgets
Version: 1.2
Release: 3
Prefix: /opt
Copyright: Commercial
Group: Application/Productivity
URL: http://www.whizbangwidgets.com/
Vendor: WhizBang Widgets
Packager: John Doe <jd@whizbangwidgets.com>
%description
This is a demonstration of a relocatable RPM package for a fictional productivity application.
%files
/opt/whizbang/bin/widgets
/opt/whizbang/man/widgets.1
/etc/opt/whizbang/widgets.conf
# Post-install stuff would go here.
%E0F
```

1. Build the RPM package for Widgets (widgets-1.2-3.i486), as shown in Example 4.2, using widgets-1.2-3.spec as the input file. You can use rpm to build and produce a source package file (widgets-1.2-3.src.rpm) and a binary package file (widgets-1.2-3.i486.rpm) from this input.

# Example 4.2: Building an RPM Package for Widgets

```
# rpm -ba /usr/src/redhat/SPECS/widgets-1.2-3.spec
Processing files: widgets
Finding provides...
Finding requires...
Prereqs: /bin/sh
Wrote: /usr/src/redhat/SRPMS/widgets-1.2-3.src.rpm
Wrote: /usr/src/redhat/RPMS/i486/widgets-1.2-3.i486.rpm
```