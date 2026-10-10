# emerge

Purpose: Install/remove Gentoo Linux packages.

Usage syntax: `emerge [OPTIONS] [PACKAGE]`

```
# emerge uptime
Calculating dependencies... done!
>>> Verifying ebuild Manifests...
>>> Emerging (1 of 1) app-vim/uptime-1.3 to /
>>> Downloading 'http://distfiles.gentoo.org/distfiles/uptime-1.3.tar.bz2'
...
```

![](bbox=[0.26, 0.32, 0.82, 0.34])

**emerge** is a front-end for Gentoo's **Portage** software manager. It provides automatic software compilation, installation, and dependency fulfillment similar to the previously discussed **aptitude** and **yum** commands.

Portage is a unique package manager in the fact that it compiles software from source code. This is different than most other Linux systems which utilize precompiled binaries when installing software. Compiling software from source code creates a platform-optimized installation that has been shown to provide better performance when compared to precompiled packages. Portage's disadvantage, however, is that it takes much longer to install software for source.

> *To learn more about the Portage software manager, see the official Gentoo documentation online at www.gentoo.org/doc/.*

Common usage examples:

+   * `emerge [PACKAGE]` Install the specified package
+   * `emerge -u world` Install the newest versions of all packages
+   * `emerge -C [PACKAGE]` Remove the specified package
+   * `emerge -s [PACKAGE]` Search for the specified package
+   * `emerge --sync` Update the portage database