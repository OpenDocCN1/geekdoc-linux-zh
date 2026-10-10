
# ENVIRONMENT VARIABLES

*PKG_CONFIG_PATH*  
A colon-separated (on Windows, semicolon-separated) list of directories to search for .pc files. The default directory will always be searched after searching the path; the default is *libdir/pkgconfig:datadir/pkgconfig* where *libdir* is the *libdir* for *pkg-config* and *datadir* is the *datadir* for *pkg-config* when it was installed.

*PKG_CONFIG_DEBUG_SPEW*  
If set, causes *pkg-config* to print all kinds of debugging information and report all errors.

*PKG_CONFIG_TOP_BUILD_DIR*  
A value to set for the magic variable *pc_top_builddir* which may appear in .pc files. If the environment variable is not set, the default value “$(top_builddir)” will be used. This variable should refer to the top builddir of the Makefile where the compile/link flags reported by *pkg-config* will be used. This only matters when compiling/linking against a package that hasn’t yet been installed.

*PKG_CONFIG_DISABLE_UNINSTALLED*  
Normally if you request the package “foo” and the package “foo-uninstalled” exists, *pkg-config* will prefer the “uninstalled” variant. This allows compilation/linking against uninstalled packages. If this environment variable is set, it disables said behavior.

*PKG_CONFIG_ALLOW_SYSTEM_CFLAGS*  
Don’t strip -I/usr/include out of cflags.

*PKG_CONFIG_ALLOW_SYSTEM_LIBS*  
Don’t strip -L/usr/lib or -L/lib out of libs.

*PKG_CONFIG_SYSROOT_DIR*  
Modify -I and -L to use the directories located in target sysroot. This option is useful when cross-compiling packages that use pkg-config to determine CFLAGS and LDFLAGS. -I and -L are modified to point to the new system root, this means that a -I/usr/include/libfoo will become -I/var/target/usr/include/libfoo with a *PKG_CONFIG_SYSROOT_DIR* equal to /var/target (same rule apply to -L).

*PKG_CONFIG_LIBDIR*  
Replaces the default *pkg-config* search directory, usually /usr/lib/pkgconfig.

# QUERYING PKG-CONFIG'S DEFAULTS

*pkg-config* can be used to query itself for the default search path, version number and other information, for instance using: `$ pkg-config --variable pc_path pkg-config` or `$ pkg-config --modversion pkg-config`

# WINDOWS SPECIALITIES

If a .pc file is found in a directory that matches the usual conventions (i.e., ends with `lib\pkgconfig` or `share\pkgconfig`), the *prefix* for that package is assumed to be the grandparent of the directory where the file was found, and the *prefix* variable is overridden for that file accordingly.

If the value of a variable in a .pc file begins with the original, non-overridden, value of the *prefix* variable, then the overridden value of *prefix* is used instead.

# AUTOCONF MACROS

```
PKG_CHECK_MODULES(VARIABLE-PREFIX, MODULES [ ACTION-IF-FOUND [ ACTION-IF-NOT-FOUND]])
```

The macro PKG_CHECK_MODULES can be used in *configure.ac* to check whether modules exist. A typical usage would be: PKG_CHECK_MODULES([MYSTUFF], [gtk+-2.0 >= 1.3.5 libxml2 >= 2.6.0])

This would result in MYSTUFF_LIBS and MYSTUFF_CFLAGS substitution variables, set to the libs and cflags for the given module list. If a module is missing or has the wrong version, by default configure will abort with a message. To replace the default action, specify an ACTION-IF-NOT-FOUND. PKG_CHECK_MODULES will not print any error messages if you specify your own ACTION-IF-NOT-FOUND. However, it will set the variable MYSTUFF_PKG_ERRORS, which you can use to display what went wrong.

Note that if there is a possibility the first call to PKG_CHECK_MODULES might not happen, you should be sure to include an explicit call to PKG_PROG_PKG_CONFIG in your configure.ac.

Also note that repeated usage of VARIABLE-PREFIX is not recommended. After the first successful usage, subsequent calls with the same VARIABLE-PREFIX will simply use the _LIBS and _CFLAGS variables set from the previous usage without calling *pkg-config* again.

```
PKG_PROG_PKG_CONFIG([MIN-VERSION])
```

Defines the PKG_CONFIG variable to the best pkg-config available, useful if you need pkg-config but don't want to use PKG_CHECK_MODULES.

```
PKG_CHECK_EXISTS(MODULES, [ACTION-IF-FOUND], [ACTION-IF-NOT-FOUND])
```

Check to see whether a particular set of modules exists. Similar to PKG_CHECK_MODULES(), but does not set variables or print errors.

Similar to PKG_CHECK_MODULES, make sure that the first instance of this or PKG_CHECK_MODULES is called, or make sure to call PKG_CHECK_EXISTS manually.

```
PKG_INSTALLDIR(DIRECTORY)
```

Substitutes the variable pkgconfdir as the location where a module should install pkg-config .pc files. By default the directory is $libdir/pkgconfig, but the default can be changed by passing DIRECTORY. The user can override through the --with-pkgconfdir parameter.

```
PKG_NOARCH_INSTALLDIR(DIRECTORY)
```

Substitutes the variable noarch_pkgconfdir as the location where a module should install arch-independent pkg-config .pc files. By default the directory is $datadir/pkgconfig, but the default can be changed by passing DIRECTORY. The user can override through the --with-noarch-pkgconfigdir parameter.

```
PKG_CHECK_VAR(VARIABLE, MODULE, CONFIG-VARIABLE, [ACTION-IF-FOUND], [ACTION-IF-NOT-FOUND])
```

Retrieves the value of the pkg-config variable CONFIG-VARIABLE from MODULE and stores it in VARIABLE. Note that repeated usage of VARIABLE is not recommended as the check will be skipped if the variable is already set.

# METADATA FILE SYNTAX

To add a library to the set of packages pkg-config knows about, simply install a .pc file. You should install this file to libdir/pkgconfig.

Here is an example file:

```
# This is a comment
prefix=/home/hp/unst
# this defines a variable
exec_prefix=${prefix}
# defining another variable in terms of the first
libdir=${exec_prefix}/lib
includedir=${prefix}/include
Name: Gooject
# human-readable name
Description: GObject/type system for GLib
# human-readable description
Version: 1.3.1
URL:
Requires: glib-2.0 >= 2.0
Conflicts: foobar <= 4.5
Libs: -L${libdir} -lgobject-1.3
Libs.private: -lm
Cflags: -I${includedir}/glib-2.0 -I${libdir}/glib/include
```

You would normally generate the file using configure, so that the prefix, etc. are set to the proper values. The GNU Autoconf manual recommends generating files like .pc files at build time rather than configure time, so when you build the .pc file is a matter of taste and preference.

Files have two kinds of line: keyword lines start with a keyword plus a colon, and variable definitions start with an alphanumeric string plus an equals sign. Keywords are defined in advance and have special meaning to pkg-config; variables do not, you can have any variables that you wish (however, users may expect to retrieve the usual directory name variables).

Note that variable references are written "${foo}"; you can escape literal "${" as "$${".

- **Name:**  
  This field should be a human-readable name for the package. Note that it is not the name passed as an argument to pkg-config.

- **Description:**  
  This should be a brief description of the package.

- **URL:**  
  An URL where people can get more information about and download the package.

- **Version:**  
  This should be the most-specific-possible package version string.

- **Requires:**  
  This is a comma-separated list of packages that are required by your package. Flags from dependent packages will be merged into the flags reported for your package. Optionally, you can specify the version of the required package (using the operators =, <, >, >=, <=); specifying a version allows pkg-config to perform extra sanity checks. You may only mention the same package once on the Requires: line. If the version of a package is unspecified, any version will be used with no checking.

- **Requires.private:**  
  A list of packages required by this package. The difference from Requires is that the packages listed under Requires.private are not taken into account when a flag list is computed for dynamically linked executable (i.e., when --static was not specified). In the situation where each .pc file corresponds to a library, Requires.private shall be used exclusively to specify the dependencies between the libraries.

- **Conflicts:**
