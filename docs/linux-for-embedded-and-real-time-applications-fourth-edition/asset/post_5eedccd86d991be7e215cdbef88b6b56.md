
## BitBake is now a sub-project of the Yocto Project.

OE-Core itself then is a base layer of recipes, classes, and associated files that is meant to be common among many different OpenEmbedded-derived systems.

There is a *Getting Started* guide in the documentation section of the OE web site. What follows is derived from that. Consult the guide for more details.

The first step is to make sure you have all of the necessary packages installed. Here is a complete list of the packages required when installing under CentOS:

- bzip2
- chrpath
- cpp
- diffstat
- diffutils
- gawk
- gcc
- gcc-c++
- git
- glibc-devel
- gzip
- make
- patch
- perl
- python
- SDL-devel
- tar
- texinfo
- unzip
- wget
- xterm

The list for other distributions is similar. In reality, most of these were installed during the original CentOS installation. Here is the command for the packages I had to install (run as root of course):

```
yum install texinfo chrpath SDL-devel
```

It turns out that the version of python in the CentOS repo is too old for OE-Core. The upshot is you have to download and install python3. Go to the python web site, download the latest, and consult the README file for instructions on installation.

To install OE-Core, execute these commands from your home directory:

```
git clone git://git.openembedded.org/openembedded-core oe-core
cd oe-core
git clone git://git.openembedded.org/bitbake bitbake
git checkout pyro
cd bitbake
git checkout 1.34
cd ..
```

The first thing to notice is that OE-core is substantially larger than buildroot: about 123 MB vs 17 MB. The next step is to initialize the build environment by executing the `oe-init-build-env` script like this:

```
source oe-init-build-env [build_dir]
```

Normally, the shell spawns a new process every time it executes a command or script. The `source` command causes the script to be executed in the current shell environment. The optional argument is the subdirectory of `oe-core/` that holds all the files created during the build. The default is `build/`. This script creates a couple of configuration files with default values, creates and changes to the `build/` directory, and adds some entries to your `PATH` environment variable. Execute `echo $PATH`, and note three new entries at the beginning. If you intend to use `OE-Core` for real, you might want to add these to the `PATH` definition in your `~/.bash_profile` file. Otherwise, you will have to run the `oe-init-build-env` script every time you want to do something with OE-Core.

One of the files just created is `build/conf/local.conf`. This provides general configuration for the images you build. Let us have a look. The file is well-commented, describing each variable. The first is the `MACHINE` for which to build images. All of the possibilities are listed as comments. There are several QEMU targets, as well as some specific hardware targets. The default is `qemux86`, the 32-bit Intel architecture running under QEMU, an open source multi-platform emulator.

Next, some directories are specified. Default values are subdirectories of `TOPDIR`, the `build/` directory:

- `DL_DIR`—where downloaded source packages are stored
- `SSTATE_DIR`—where *shared state* files are stored. This speeds up subsequent builds
- `TMPDIR`—where build output is stored

We can specify which package management format to use with the `PACKAGE_CLASSES` variable. Unless you are building for a "debian flavor" distro, you should probably select rpm.

Save `local.conf`, and we are ready to build a cross-tool chain and a set of images. OE-Core provides a set of predefined targets that we can use to build our own images. A couple of these were listed by `oe-init-build-env`. To see the complete set of image targets execute:

```
ls .../meta/*-recipes*/images/*.bb
```

Now to build the `core-image-minimal` image, we simply execute:

```
bitbake core-image-minimal
```

## OE Metadata

While the image is “baking,” it is an opportunity to explore OE metadata. The `metadata` that drives BitBake consists of recipes and configuration files. Recipes get the file extension `*.bb`, and configuration files get the extension `.conf`. All of this metadata resides in the subdirectory `meta/`. Although it is not obvious from the layout of `meta/`, the recipes are divided into a hierarchy of four categories:

- Image
- Task
- Package
- Class

The motivation for the hierarchical organization is that recipes in lower levels can be easily reused.

Image is the top level of the hierarchy. An image recipe defines what goes into a specific root file system image. It lists the tasks that make up the image. Have a look at `meta/recipes-core/images/core-image-minimal.bb`. It installs one task, `packagegroup-core-boot`, and possibly others defined in `CORE_IMAGE_EXTRA_INSTALL`. It also inherits a class called `core-image`. Class files get the extension `.bbclass`, and reside in `meta/classes/`.

Task recipes typically represent aggregations of packages. In fact, many of them are named `packagegroup-*`. For example take a look at `packagegroup-core-boot.bb`. It claims to be “The minimal set of packages required to boot the system.” Among other things, it inherits a class called `packagegroup`.

A package recipe manages the specific needs of an individual package. Package recipes typically have a version number appended to the name. `meta/recipes-core/sysvinit/sysvinit_2.88dsf.bb` is a typical example. It identifies where the package is found on the net, the license terms, the required files, and so on.

Class recipes have a peer-to-peer relationship with the other recipes, rather than a hierarchical one. They are used to factor out common recipe elements that can then be reused, through the inherit command. The most frequent use of classes is to inherit functions or portions of recipes for commonly used build tools like the GNU autotools. Have a look at `meta/classes/core-image.bbclass`. It in turn inherits `image.bbclass`.

## Testing the New Image: Quick EMUlator

How do we test our newly created image? OE-Core includes a tool called QEMU, which stands for Quick EMUlator. QEMU is an open source project that emulates several different machine architectures. The image we just built is for the x86 running under QEMU, and is named qemu-x86. So to test it, all we have to say is:

```
runqemu qemu-x86
```

## Personal Observations

Personally, I do not care much for Open Embedded, or the Yocto Project that we will look at next. They are simply too big, too complex, too obscure. The learning curve is steeper than for Linux itself. To quote the introductory paper listed in Resources:

> "[I]t has a considerable learning curve and the source of build errors may not be obvious. Development teams that are unfamiliar with OE should allow at least several weeks to attain moderate proficiency."

It is not the least bit obvious how you would modify any of the over 4000 files in the `meta/` directory to effect any meaningful change in your root file system image. As far as I can tell, there is no graphical configuration tool.

## Yocto Project

The Yocto Project is a collaborative effort of the Linux Foundation. The goal is to produce tools and processes that will facilitate creating Linux distributions for embedded software that are independent of the underlying architecture of the embedded software itself. The project was announced by the Linux Foundation in 2010, and in March 2011, the project aligned itself with Open Embedded to create The OpenEmbedded-Core Project. Yocto’s reference implementation of OE-Core is called Poky (pronounced PAH-kee, not POH-kee).

Yocto appears to be somewhat more comprehensive than OE-Core. Fig. 13.3 shows the Yocto workflow.

## Integrated build environments

![](img/f03d6fa2c5faefc793771df52bbb2ef9_221_0.png)

Figure 13.3

Yocto Project development environment.

The Poky build system is available in two forms: as a git repository or as a single Bzip file. `cd` to your home directory and do one of the following:

```
git clone -b pyro git://git.yoctoproject.org/poky.git
git checkout pyro
```

Download `poky-pyro-17.0.0.tar.bz2` from the Yocto Project downloads page and untar it. For simplicity, rename the directory `poky-pyro-17.0.0` as just `poky`.

This time we will build an image for the BBB. That requires editing `poky/build/local.conf` to change the target machine. Find the line `#MACHINE ?= "beaglebone"` and remove the leading hash mark. Save the file.

The process for building an image is very much like OE-Core. We first have to initialize the build environment:

```
source oe-init-build-env
```

Let us build something just a little more ambitious this time:

```
bitbake core-image-full-cmdline
```

## Application Development with Yocto: The Software Development Kit and Eclipse

So far we have talked about building bootloaders, kernels, root file systems, and tool chains, but we have not said anything about application development, which is probably
