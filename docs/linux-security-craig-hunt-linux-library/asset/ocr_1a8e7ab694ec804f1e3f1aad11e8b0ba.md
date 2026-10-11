drwxr-x--- 2 ramon users 1024 Mar 1 1998 plug-gw
drwxr-x--- 2 ramon users 1024 Mar 1 1998 rlogin-gw
drwxr-x--- 2 ramon users 1024 Mar 1 1998 snapd
drwxr-x--- 2 ramon users 1024 Mar 1 1998 snapd
-rw-r-- 1 ramon users 5526 Mar 26 1996 syssexits.h
drwxr-x--- 2 ramon users 1024 Mar 1 1998 tn-gw
drwxr-x--- 5 ramon users 1024 Jan 18 1997 tools
drwxr-x--- 2 ramon users 1024 Mar 1 1998 x-gw

As you can see, the FTWK distribution includes a number of preconfigured `Makefile.config` examples for several popular operating systems, including Linux. Note also that the source code for each of the proxies (ft p-gw, http-gw, etc.) is housed in a different subdirectory. Start by preserving the original `Makefile.config` file and moving the supplied `Makefile.config.linux` file in its place using the following commands:

```
```console
[ramon]$ mv Makefile.config Makefile.config.ORIG
[ramon]$ cp Makefile.config.linux Makefile.config
```

```

> **TIP** If you’re building FTWK on Red Hat 7.0, you’ll have to edit the resulting `Makefile.config` file and change the value of the `XLIBDIR` variable from `/usr/X11/lib` to `/usr/X11R6/lib.`. In addition, you’ll have to set the value of `AUXLIB` to `~/lcrypt` and the value of `DBMLIB` to `~/ndbm`.

You’re now ready to compile, link, and install the package using the following two commands:

```
```console
[ramon]$ make
[ramon]$ sudo make install
```

```

I found that the man pages do not get installed by default, so I copied them in place by hand:

```
```console
[ramon]$ cd doc/man
[ramon]$ sudo cp *.8 /usr/share/man/man8/
[ramon]$ sudo cp *.5 /usr/share/man/man5/
[ramon]$ sudo cp *.3 /usr/share/man/man3/
```

```

The FTWK package installs both its executables and configuration files in the `/usr/local/etc` directory tree. Here’s what this directory should look like once the FTWK package is completely installed:

```
```console
[ramon]$ ls -1 /usr/local/etc
```

```