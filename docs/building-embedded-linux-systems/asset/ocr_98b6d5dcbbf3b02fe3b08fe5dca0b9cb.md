ports for architectures glibc does not support (such as Blackfin and FRV), but is based on the latest code from glibc, so it may be the only choice for the newer ports (such as Alpha, AMD64, and HPPA).

# *LARGE file support*

Enabling this option allows uClibc to support files larger then 2 GB, at the expense of a bigger footprint.

# *Malloc implementation*

This submenu allows a choice between three `malloc()` implementations, ranging from a simplistic implementation suitable for systems with smaller RAM and allocations up to a standard implementation equivalent to the one found in glibc.

# *Malloc returns live pointer for malloc(0)*

This option controls the behavior of `malloc()` when asked to return an allocation of zero size. Enable this option for full glibc compatibility.

# *Dynamic atexit() support*

Controls whether to support multiple dynamic `atexit()` callbacks. Required for proper C++ support.

# *Old (visible) atexit support*

An outdated option included for backward compatibility with older releases of uClibc. Leave unset.

# *Enable SuSv3 LEGACY functions and enable SuSv3 LEGACY macros*

Enable support for defunct functions and macros (**bcopy**, **bzero**, **bcmp**, **index**, and **rindex**) that some software packages might still need.

# *Shadow password support*

Enable support for keeping the user password in a shadow file, separate from the master user database, for better security. This option is recommended.

# *Support for program_invocation_name and support for __progname*

These options enable support for very rarely used aliases to the `argv[0]` argument containing a program name. Some software packages (notably GNU `tar` and coreutils) use these aliases to provide extra useful output. It is normally safe to leave this option unset.

# *Supports only Unix 98 PTYs*

Unsetting this option enables legacy support for non-Unix 98 PTYs. Unless you are going to use older applications, it is safe to leave this set.

# *Assume that /dev/pts is a devfs or devfs filesystem*

Enabling this option assumes that the devpts virtual filesystem is used to keep track of pseudo-terminal devices. This is normally true for modern Linux systems. But if you choose this option, enable devpts support in the kernel configuration.

# *Various additional time related options*

The last options in this menu control the handling of time and time zones in uClibc. For full glibc compatibility and best performance, you should turn on all these options.