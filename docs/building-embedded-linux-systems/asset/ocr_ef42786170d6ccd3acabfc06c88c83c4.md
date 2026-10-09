binary a derived work and can distribute it only under the terms of the GPL. A commercial license is available from the package's main author if you wish to distribute non-GPL code linked with diet libc. If, however, you would prefer not to have to deal with such licensing issues, you may want to use uClibc instead.

Diet libc is available for download both as a tar-bzip2'd archive or using CVS from the project's website at http://www.fefe.de/dietlibc/ . The package comes with an FAQ and installation instructions. In the following examples, we will use version 0.21 of diet libc, but the explanations should apply to other versions as well.

# Library setup

As with uClibc, the first step to setting up diet libc is to download it into your $[P|R]OOT]/build-tools directory. Here, too, you will build the library within the package's source directory and not in another directory, as was the case for the GNU toolchain. No configuration is required for diet libc. Instead, you can proceed with the build stage immediately.

Once the package is extracted, move into the *diet libc* directory for the setup:

```
$ cd $[P|R]OOT]/build-tools/dietlibc-0.31
```

Before building the package for your target, build it for your host. This is necessary to create the *diet* utility, which is required to build diet libc for the target and later to build applications against diet libc:

```
$ make
```

In the setup used for this example, this command creates a *bin-ppc* directory containing a PPC diet libc. You can now compile diet libc for your target:

```
$ make ARCH=i386 CROSS=i386-linux-
```

You will see even more warnings than with the other packages, but you can ignore them. Here, you must tell the Makefile both the architecture for which diet libc is built and the prefix of the cross-platform development tools.

With the package now built, you can install it:

```
$ make ARCH=i386 DESTDIR=5$(PREFIX)/dietlibc prefix="" install
```

This installs diet libc components in $(PREFIX)/dietlibc. Again, as when building the package for your target, you must specify the architecture. Also specify the install destination using the *DESTDIR* variable, and reset the Makefile's internal *prefix* variable, which is different from the capital *PREFIX* environment variable.