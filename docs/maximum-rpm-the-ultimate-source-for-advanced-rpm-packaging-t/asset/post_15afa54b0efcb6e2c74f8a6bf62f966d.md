
# rpm -qip foo-client-2.7-1.i386.rpm
Name    : foo-client
Version : 2.7
Release : 1
Install date: (none)
Group   : bogus/junque
Size    : 42
Summary : The foo client
Description:
This is the long description for the foo client...
Distribution: (none)
Vendor: (none)
Build Date: Wed Nov 06 13:33:37 1996
Build Host: foonly.rpm.org
Source RPM: foo-2.7-1.src.rpm

# rpm -qip bazlib-5.6-1.i386.rpm
Name    : bazlib
Version : 5.6
Release : 1
Install date: (none)
Group   : bogus/junque
Size    : 38
Summary : The baz library
Description:
This is the long description for the bazlib...
#

Here we’ve used RPM’s query capability to display a list of summary information for each package. A few points are worth noting.

First, each package lists `foo-2.7-1.src.rpm` as its source package file. This is the only way to tell if two package files were created from the same set of sources. Trying to use a package’s name as an indicator is futile, as the `bazlib` package shows us.

The next thing to notice is that the summaries and descriptions for each package are specific to that package. Since these tags were placed and named according to each package, this should be no surprise.

Finally, we can see that each package’s version has been either inherited from the main package’s preamble or, as in the case of the `bazlib` package, the main package’s version has been overrid-den by a version tag added to `bazlib`’s preamble.

If we look at the source package’s information, we see that its information has been taken entirely from the main package’s set of tags:

# rpm -qip foo-2.7-1.src.rpm
Name    : foo
Version : 2.7
Release : 1
Install date: (none)
Group   : bogus/junque
Size    : 1415
Summary : The foo app, and the baz library needed to build it
Description:
This is the long description of the foo app, and the baz library needed to build it...
#
Distribution: (none)
Vendor: (none)
Build Date: Wed Nov 06 13:33:37 1996
Build Host: foonly.rpm.org
Source RPM: (none)

It's easy to see that if there were no `%files` list for the main package, and therefore, no main package, the tags in the main preamble would still be used in the source package. This is why RPM enforces the requirement that the main preamble contain copyright, `%description`, and group tags. So, here's a word to the wise: Don't put something stupid in the main preamble's `%description` just to satisfy RPM. Your witty saying will be immortalized for all time in every source package you distribute. (Yes, the author found out about this the hard way!)

### 18.6.1.1. Verifying Subpackage-Specific Install and Erase Scripts

The easiest way to verify that the %pre scripts we defined for each package were actually used is to simply install each package:

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

As expected, the unique %pre script for each package has been included. Of course, if we hadn't wanted to actually install the packages, we could have used RPM's `--scripts` option to display the scripts:

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

This approach might be a bit safer, particularly if installing the newly built package would disrupt operations on your build system.

# Building Packages for Multiple Architectures and Operating Systems

While RPM certainly makes packaging software as easy as possible, it doesn't stop there. RPM gives you the tools you need to build a package on different types of computers. More importantly, RPM makes it possible to build packages on different types of computers using a single spec file. Those of you who have developed software for different computers know the importance of maintaining a single set of sources. RPM lets you continue that practice through the package-building phase.

Before we get into RPM's capabilities, let's quickly review what is involved in developing software for different types of computer systems.

### 19.1. Architectures and Operating Systems: A Primer

From a software engineering standpoint, there are only two major differences between any two computer systems:

- The architecture implemented by the computer's hardware
- The system software running on the computer

The first difference is built into the computer. The architecture is the manner in which the computer system was designed. It includes the number and type of registers present in the processor, the number of machine instructions, what operations they perform, and so on. For example, every PC today, no matter who built it, is based on the Intel x86 architecture.

The second difference is more under our control. The operating system is software that controls how the system operates. Different operating systems have different methods of storing information on disk, different ways of implementing functions used by programs, and different hardware requirements.

As far as package building is concerned, two systems with the same architecture running two different operating systems are as different as two systems with different architectures running the same operating system. In the first case, the software being packaged for the different operating systems will differ due to the differences between the operating systems. In the second case, the software being packaged for different architectures will differ due to the underlying differences in hardware. (This is a somewhat simplistic view of the matter; it's common for incompatibilities to crop up between two different implementations of the same operating system on different architectures.)

RPM supports differences in architecture and operating system equally. If there is a tag, rpmrc file entry, or conditional that is used to support architectural differences, there is a corresponding tag, entry, or conditional that supports operating system differences.

### 19.1.1. Let's Just Call Them Platforms

In order to keep the duplication in this chapter to a minimum, we'll refer to a computer of a given architecture running a given operating system as a *platform*. If another system differs in either aspect, it is considered a different platform.

Okay, now that we've gotten through the preliminaries, let's look at RPM's multiplatform capabilities.

### 19.2. What Does RPM Do to Make Multiplatform Packaging Easier?

As we mentioned, RPM supports multiplatform package building through a set of tags, *rpmrc* file entries, and conditionals. None of these tools is difficult to use. In fact, the hardest part of multiplatform package building is figuring out how the software needs to be changed to support different platforms.

Let's take a look at each multiplatform tool RPM provides.

### 19.2.1. Automatic Detection of the Build Platform

The first thing necessary for easy multiplatform package building is to identify which *platform the package* is to be built for. Except in the fairly esoteric case of cross-compilation, the *build platform* is the platform on which the package is built. RPM does this for you automatically, although it can be overridden at build time.

### 19.2.2. Automatic Detection of the Install Platform

The other important *platform* in package building is the platform on which the package is to be installed. Here again, RPM does this for you, although it's possible to override this when the package is installed.

But there is more to multiplatform package building than simply being able to determine the *platform* during package building and installation. The next component in multiplatform package building is a set of *platform-dependent* tags.

### 19.2.3. Platform-Dependent Tags

RPM uses a number of *tags* that control which platforms can build a package. These *tags* make it easier for the package builder to build multiple packages automatically since the *tags* keep RPM from attempting to build packages that are incompatible with the build *platform*.
