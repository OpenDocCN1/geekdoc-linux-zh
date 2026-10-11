well. Using the subpackage structure from our sample spec file, we would end up with script definitions like this:

```
%pre server
%postun client
%preun -n bazlib
%verifyscript client
```

Other than the change in naming, there's only one thing to be aware of when creating scripts for subpackages. It's important that you consider the possibility of scripts from various subpackages interacting with each other. Of course, this is simply good script-writing practice, even if the packages involved are not related.

# 18.4.3.1. Back at the Spec File

Here we've added some scripts to our spec file. So that our example doesn't get too complex, we've just added preinstall scripts for each package:

```
Name: foo
Version: 2.7
Release: 1
Source: foo-2.7.tgz
Copyright: probably not
Summary: The foo app, and the baz library needed to build it
Group: bogus/junque
%description
This is the long description of the foo app, and the baz library needed to
build it...
%package server
Summary: The foo server
Group: bogus/junque
%description server
This is the long description for the foo server...
%package client
Summary: The foo client
Group: bogus/junque
%description client
This is the long description for the foo client...
%package -n bazlib
Version: 5.6
Summary: The baz library
Group: bogus/junque
%description -n bazlib
This is the long description for the bazlib...
%pre
echo "This is the foo package preinstall script"
%pre server
echo "This is the foo-server subpackage preinstall script"
```