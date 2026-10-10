# ENVIRONMENT VARIABLES

*PKG_CONFIG_PATH*
A colon-separated (on Windows, semicolon-separated) list of directories to search for .pc files. The default directory will always be searched after searching the path; the default is *libdir/pkgconfig:datadir/pkgconfig* where *libdir* is the *libdir* for *pkg-config* and *datadir* is the *datadir* for *pkg-config* when it was installed.

*PKG_CONFIG_DEBUG_SPEW*
If set, causes *pkg-config* to print all kinds of debugging information and report all errors.

*PKG_CONFIG_TOP_BUILD_DIR*
A value to set for the magic variable *pc_top_builddir* which may appear in .pc files. If the environmt variable is not set, the default value “$(top_builddir)” will be used. This variable should refer to the top builddir of the Makefile where the compile/link flags reported by *pkg-config* will be used. This only matters when compiling/linking against a package that hasn’t yet been installed.

*PKG_CONFIG_DISABLE_UNINSTALLED*
Normally if you request the package “foo” and the package “foo-uninstalled” exists, *pkg-config* will prefer the “uninstalled” variant. This allows compilation/linking against uninstalled packages. If this environmt variable is set, it disables said behavior.

*PKG_CONFIG_ALLOW_SYSTEM_CFLAGS*
Don’t strip -I/usr/include out of cflags.

*PKG_CONFIG_ALLOW_SYSTEM_LIBS*
Don’t strip -L/usr/lib or -L/lib out of libs.

*PKG_CONFIG_SYSROOT_DIR*
Modify -I and -L to use the directories located in target sysroot. this option is useful when cross-compiling packages that use pkg-config to determine CFLAGS and LDFLAGS. -I and -L are modified to point to the new system root, this ans that a -I/usr/include/libfoo will beco -I/var/target/usr/include/libfoo with a *PKG_CONFIG_SYSROOT_DIR* equal to /var/target (sa rule apply to -L)

*PKG_CONFIG_LIBDIR*
Replaces the default *pkg-config* search directory, usually /usr/lib/pkgconfig