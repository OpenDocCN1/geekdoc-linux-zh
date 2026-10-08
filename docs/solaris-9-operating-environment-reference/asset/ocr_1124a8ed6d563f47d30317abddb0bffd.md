# 1546

# whereis

# Description

whereis locates source binary and manual sections for specified files. The supplied names are first stripped of leading path-name components and any (single) trailing extension of the form .ext, .c. Prefixes of s, resulting from the use of source code control are also stripped. whereis then tries to locate the desired program in a list of standard places:

+   * /usr/bin
* /usr/bin
* /usr/sbin
* /usr/games
* /usr/hosts
* /usr/include
* /usr/local
* /usr/etc
* /usr/lib
* /usr/share/man
* /usr/src
* /usr/ucb

# Options

+   * -b Search only for binaries.
* -B Change or otherwise limit the places whereis searches for binaries.
* -f Terminate the last directory list and signal the start of file names. You must use this option with any of the -B, -M, or -S options.
* -m Search only for manual sections.
* -M Change or otherwise limit the places whereis searches for sections.
* -s Search only for sources.
* -S Change or otherwise limit the places whereis searches for sources.
* -u Search for unusual sources. A file is unusual if it does not have one entry of each requested type. Thus, whereis -u * asks for files in the current directory that has no documentation.

# Examples

The following example finds the location of all files named libc.

```
castle@ whereis libc
libc:/usr/lib/libc.so /usr/lib/libc2.so /usr/lib/libc2.a
/usr/lib/libc.a
castle@
```

The following example finds all files in /usr/ucb with source in /usr/src/cmd that are not documented in /usr/share/man/man.

```
castle@ cd /usr/ucb
castle@ whereis -M /usr/share/man/man1 -S /usr/src/cmd -f *
Mail:/usr/ucb/Mail
adplot:/usr/ucb/adplot
arch:/usr/bin/arch /usr/ucb/arch
```