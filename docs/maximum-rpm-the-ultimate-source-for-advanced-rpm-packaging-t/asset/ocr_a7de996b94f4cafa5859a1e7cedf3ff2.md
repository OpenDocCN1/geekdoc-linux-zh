Since the baz library's package name is not to start with foo, we need to use the -n option on its %package directive:

```
%package -n bazlib
```

Our requirements further state that foo-server and foo-client are to have the same version as the main package.

One of the time-saving aspects of using subpackages is that there is no need to duplicate information for each subpackage if it is already defined in the main package. Therefore, since the main package's preamble has a version tag defining the version as 2.7, the two subpackages that lack a version tag in their preambles will simply inherit the main package's version definition.

Since the bazlib subpackage's preamble contains a version tag, it must have its own unique version.

In addition, each subpackage must have its own summary tag.

So, based on these requirements, our spec file now looks like this:

```
Name: foo
Version: 2.7
Release: 1
Source: foo-2.7.tgz
CopyRight: probably not
Summary: The foo app, and the baz library needed to build it
Group: bogus/junk
%description
This is the long description of the foo app, and the baz library needed to build it...

%package server
Summary: The foo server

%package client
Summary: The foo client

%package -n bazlib
Version: 5.6
Summary: The baz library
```

We can see the subpackage structure starting to appear now.

# 18.4.1.4. Required Tags in Subpackages

There are a few more tags we should add to the subpackages in our sample spec file. In fact, if these tags are not present, RPM will issue a most impressive warning:

```
# rpm -ba foo-2.7.spec
Package: foo-server
Field must be present: Description
Field must be present: Group
```