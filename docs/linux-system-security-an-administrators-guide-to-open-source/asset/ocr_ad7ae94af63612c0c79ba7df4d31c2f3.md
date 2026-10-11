# Building xinetd

After you have downloaded and built the source tree for xinetd, you will find a **configure** script for the purpose of building the **Makefile** and related files for compilation and linking (see *Implementing Version 1.5.9p4* on page 175 in Chapter 9 for a more detailed discussion of the configure utility). This implementation of configure utilizes only a few options. You may view the available options with **configure --help**.

By default, the xinetd configure utility uses /usr/local as its destination root directory. If you wish to use a different root directory, you may do so with the **--prefix** option. Example 10-35 uses **--prefix=/usr** and the **--with-libwrap** (the latter for incorporating **libwrap** access control) options. Also, this example uses /usr/src/xinetd as the build directory.

# Example 10-35 Using configure for xinetd

```
```
# ./configure --prefix=/usr --with-libwrap
creating cache ./config.cache
checking host system type... i686-pc-linux-gnu
checking target system type... i686-pc-linux-gnu
checking build system type... i686-pc-linux-gnu
checking for gcc... gcc
checking whether the C compiler (gcc ) works... yes
<lots of output snipped>
checking for netdb.h... yes
updating cache ./config.cache
creating ./config.status
creating Makefile
#
```
```

Now that the **Makefile** is built, we can proceed with creating the bin-aries. The output of the make execution is displayed in Example 10-36.

# Example 10-36 Compiling and Linking xinetd

```
```
# make
for lib in sio str misc xlog pset ; do

(cd libs/$lib ; make install LIBDIR=/usr/src/xinetd/1ibs/lib
INCLUDEDIR=/usr/src/xinetd/lib/include MANDIR=/usr/src/xinetd/lib/man
`INSTALL/$(lib)/install" -c" ; DEFS= -DHAVE_LIBCRYPT=1 -DHAVE_UNISTD_H=1 -
DHAVE_GETPAGESIZE=1 -DHAVE_MCAP=1 -DHAWE_LIBCRYPT=1 -DHAVE_MEMCPY=1 -
DHA VE_WAITPID=1 -DHA VE SIGVEC=1 -DHA VE_SETSID=1 -DHA VE_STRTFTIME=1 -
DST DC_HEADERS=1 -DROK=4 -DHA VE_SYS_FILE_H=1 -DHA VE_FTW_H=1 -DHA VE_LINUX_TIME_H=1
" RANLIB=${"RANLIB:-ranlib"} ; CC="gcc" DEBUG=-O )
; done
<lots of output snipped>
gcc -O -o xinetd access.o addr.o builtins.o child.o conf.o confparse.o
connection.o env.o flags.o ident.o init.o int.o intcommon.o internals.o log.o
logctl.o main.o msg.o nvlists.o parse.o parseup.o parsers.o reconfig.o retry.o
sconf.o server.o service.o shutdown.o signals.o special.o tcpinet.o time.o
udpaint.o util.o redirect.o options.o -L/usr/src/xinetd/xinetd-2.1.8.5/lib/ib -
ls io -lstr -l misc -l xlog -l ipset -l crypt
# rm -f xinetd
make[1]: Leaving directory `/usr/src/xinetd/xinetd'
#
```
```