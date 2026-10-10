# Integrated build environments

![](bbox=[0.15, 0.08, 0.95, 0.38])

Figure 13.3

Yocto Project development environment.

The Poky build system is available in two forms: as a git repository or as a single Bzip file. `cd` to your home directory and do one of the following:

```
```
git clone -b pyro git://git.yoctoproject.org/poky.git
git checkout pyro
```
```

Download `poky-pyro-17.0.0.tar.bz2` from the Yocto Project downloads page and untar it. For simplicity, rename the directory `poky-pyro-17.0.0` as just `poky`.

This time we will build an image for the BBB. That requires editing `poky/build/local.conf` to change the target machine. Find the line `#MACHINE ?= "beaglebone"` and remove the leading hash mark. Save the file.

The process for building an image is very much like OE-Core. We first have to initialize the build environment:

```
```
source oe-init-build-env
```
```

Let us build something just a little more ambitious this time:

```
```
bitbake core-image-full-cmdline
```
```

# Application Development with Yocto: The Software Development Kit and Eclipse

So far we have talked about building bootloaders, kernels, root file systems, and tool chains, but we have not said anything about application development, which is probably