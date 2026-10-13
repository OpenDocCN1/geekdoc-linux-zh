# Dealing with SunOS

SunOS is the name of the UNIX operating system developed by Sun Microsystems. SunOS was originally based on BSD UNIX but has since changed to be based on System V UNIX. Although the marketing name has been changed to Solaris, uname still produces the output SunOS. Shell scripts that have to run on both Solaris and earlier BSD-based versions of SunOS, such as SunOS4, need to differentiate between these two versions.

To determine whether a system is running Solaris or SunOS, you can check the version of the operating system. SunOS versions 5 and higher are Solaris (System V-based); SunOS versions 4 and lower are SunOS (BSD-based).

To determine the version of the operating system, you can use the -r option of uname:

```
$ uname -r
5.5.1
```

This indicates that the version of the operating system is 5.5.1. If you want to add the operating system's name to this output, use the -r and the -s options:

```
$ uname -rs
SunOS 5.5.1
```

This indicates the machine is running Solaris. The output on a machine running BSD-based SunOS4 might be

```
SunOS 4.1.3
```

# Determining the Hardware Type

Sometimes a shell script is written as a wrapper around a hardware-specific program. For example, install scripts are usually the same for different hardware platforms supported by a particular operating system. Although the install script might be the same for every hardware platform, the files that are installed are usually different.

To determine the hardware type, you can use the -m option:

```
$ uname -m
sun4m
```

Some common return values and their hardware types are listed in Table 23.4.

**Table 23.4 Hardware Types Returned by the uname Command**

| Hardware | Description |
|---|---|
| 9800/xxx | Hewlett-Packard 9000 series workstation. Some common values of xxx are 700, 712, 715, and 750. |
| 1396 | Intel 386-, 486-, Pentium-, or Pentium II-based workstation. |