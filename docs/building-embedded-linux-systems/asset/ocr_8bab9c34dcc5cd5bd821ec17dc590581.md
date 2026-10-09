its main approach is to provide one small binary for each command. embutil5 was written and is maintained by Felix von Leitner, the author of diet libc, with goals very similar to those of diet libc. embutil5 is available at http://www.fefe.de/embtils/.

Though it supports many of the most common Unix commands, embtils is still far from being as exhaustive as BusyBox. For example, at the time of this writing, version 0.18 still lacks *fbset, find, grep, ifconfig, ps*, and *route*. It doesn’t offer any shell command either.

As with BusyBox, not all the options provided by the full commands are supported, but the subset provided is sufficient for most system operations. In contrast to BusyBox, however, embutil5 must be statically linked with diet libc. It can’t be linked to any other library. Because diet libc is already very small, the resulting command binaries are reasonably small, too. This can make embutil5 a better choice than BusyBox when just a few binaries are needed, because the overall size is smaller.

# # Setup

Before you start the setup, you will need to have diet libc installed on your host system, as described in Chapter 4. Then, download embtils and extract it into your ${PROJECTROOT}/sysapps directory. For this example, we use embutil5 0.18. You can move into the package’s directory for the rest of the setup:

```
$ cd ${PROJECTROOT}/sysapps/embtils-0.18
```

There is no configuration capability for embtils. You can, therefore, build the package right away:

```
$ make ARCH=ppc CROSS=powerpc-linux- all
```

You can then install embutil5:

```
$ make ARCH=ppc DESTDIR=\$\${PROJECTROOT\}\}/rootfs prefix=\"\" install
```

The options and variables used in the build and installation of embtil5 have the same meaning as those used for diet libc.

# # Usage

The embtils installation procedure copies quite a few statically linked binaries to your target root filesystem’s /bin directory. In contrast to BusyBox, this is the only directory where binaries are installed.

A BusyBox-like all-in-one binary has also been installed, allinone. This binary reacts the same way as BusyBox when proper symbolic links are created to it. Note that unlike BusyBox, you need to create these symbolic links manually, because they are not created automatically by the installation scripts. allinone supports the following commands, as revealed by the allinone.c file:

+   * As with diet libc, the trailing slash (`/`) is important.