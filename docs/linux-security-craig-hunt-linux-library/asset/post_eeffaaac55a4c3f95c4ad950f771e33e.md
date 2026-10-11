
If you prefer to compile the SOCKS5 software yourself, the next section describes how to configure and compile SOCKS5 from the source distribution.

## Compiling the Latest SOCKS5 Release

The SOCKS5 Linux distribution can be downloaded in source format from NEC's Web site at http://www. socks.nec.com/cgi-bin/download.pl (see Figure 10.2).

![](img/3258bbaf790525f8c4eb25fabff7844a_299_0.png)

In addition to the freely available reference implementation, NEC's NSL offers a fully supported commercial SOCKS5 product named e-Border. More information on e-Border, including how to download it, is available at http://www.socks5.nec.com (see Figure 10.3).

### Figure 10.3 NEC's e-Border: a commercial SOCKS5 implementation

![](img/3258bbaf790525f8c4eb25fabff7844a_300_0.png)

Once you have downloaded the gnu-zipped distribution file, proceed to unzipping and expanding the archive using the steps in Listing 10.1.

### Listing 10.1 Creating the SOCKS5 source code directories

```bash
[ramon]$ ls
socks5-v1.0r11.tar.gz

[ramon]$ gunzip socks5-v1.0r11.tar.gz
[ramon]$ ls
socks5-v1.0r11.tar
[ramon]$ tar xf socks5-v1.0r11.tar
[ramon]$ cd socks5-v1.0r11
[ramon]$ ls -l
total 234
-rw-rw- 1 ramon users 22907 Aug 16 11:38 ChangeLog
-rw-rw- 1 ramon users 3495 Feb 3 1999 Copyright
-rw-rw- 1 ramon users 4753 Jul 16 1998 INSTALL
-rw-rw- 1 ramon users 3439 Oct 20 1999 Makefile.in
-rw-rw- 1 ramon users 10883 Feb 4 1999 README
-rw-rw- 1 ramon users 2454 May 27 1999 acconfig.h
-rw-rw- 1 ramon users 10692 May 27 1999 aconfig.m4
drwxr-xr-x 7 ramon users 1024 Aug 16 11:38 clients
-rwxr-xr-x 1 ramon users 148397 Aug 2 1999 configure
-rw-rw- 1 ramon users 9885 Aug 2 1999 configure.in
drwxr-xr-x 2 ramon users 1024 Aug 16 11:38 doc
drwxr-xr-x 2 ramon users 1024 Aug 16 11:38 examples
drwxr-xr-x 2 ramon users 1024 Aug 16 11:38 include
-rwxr-xr-x 1 ramon users 4772 Jan 25 1999 install-sh
drwxr-xr-x 2 ramon users 1024 Aug 16 11:38 lib
drwxr-xr-x 4 ramon users 1024 Aug 16 11:38 man
drwxr-xr-x 2 ramon users 1024 Aug 16 11:38 patches
drwxr-xr-x 2 ramon users 1024 Aug 16 11:38 server
drwxr-xr-x 2 ramon users 1024 Aug 16 11:38 shlib
-rw-rw- 1 ramon users 29 Nov 15 1996 stamp-h.in
drwxr-xr-x 2 ramon users 1024 Aug 16 11:38 test
```

In this version of SOCKS5 (v1.0, release 11) there are ten subdirectories:

- **clients**: Sample Linux SOCKS5 clients
- **doc**: General product documentation
- **examples**: Sample configuration files
- **include**: Header files
- **lib**: Source code for the SOCKS5 static libraries
- **man**: Manual pages
- **patches**: Separate (and optional) patches to the source
- **server**: Source code for the SOCKS5 server
- **shlib**: Source code for the shared SOCKS5 libraries

In addition, there are a number of release information files (for example, ChangeLog and Copyright), a README document, and a shell script file named configure, which is the topic of the next section of this book.

Once the files have been successfully extracted in the new socks5-v1.0r11 directory, you're ready to build the SOCKS5 daemon.

> **NOTE** You need an ANSI-compatible C compiler to compile and install the SOCKS5 distribution. The GNU gcc compiler provided with your Linux distribution should work fine.

Most source distributions of software packages offer users a number of options that allow you to customize the package to your environment. The following section describes the options available for configuring the SOCKS5 source before compilation.

## Linux Compilation Parameters

Look for the configure shell script in the main source directory:

```bash
[ramon]$ ls -l configure
-rwxr-xr-x 1 ramon users 148397 Aug 2 1999 configure
```

Run the configure script with no command-line options to create a default set of compilation files, as shown in Listing 10.2.

### Listing 10.2 Executing the SOCKS5 configure script

```bash
[ramon] $ ./configure
loading cache ./config.cache
checking for gcc2... (cached) gcc
checking for gcc... (cached) gcc
checking whether the C compiler (gcc ) works... yes
checking whether the C compiler (gcc ) is a cross-compiler... no
checking whether we are using GNU C... (cached) yes
checking whether gcc accepts -g... (cached) yes
checking how to run the C preprocessor... (cached) gcc -E
checking whether gcc needs -traditional... (cached) no
checking for working const... (cached) yes
checking for inline... (cached) inline
checking for ranlib... (cached) ranlib
checking for a BSD compatible install... (cached) /usr/bin/install -c
checking for makedepend... (cached) true
checking for autoconf... (cached) autoconf
checking for autoheader... (cached) autoheader
checking for fcntl.h... (cached) yes
checking for memory.h... (cached) yes
checking for unistd.h... (cached) yes
checking for string.h... (cached) yes
checking for strings.h... (cached) yes
checking for bstring.h... (cached) no
checking for varargs.h... (cached) yes
checking for stdarg.h... (cached) yes
checking for stdlib.h... (cached) yes
checking for time.h... (cached) yes
checking for syslog.h... (cached) yes
checking for ifaddrs.h... (cached) no
checking for crypt.h... (cached) yes
checking for sys/stat.h... (cached) yes
checking for sys/param.h... (cached) yes
checking for sys/signal.h... (cached) yes
checking for sys/resource.h... (cached) yes
checking for sys/socket.h... (cached) yes
checking for sys/utio.h... (cached) yes
checking for sys/time.h... (cached) yes
checking for sys/wait.h... (cached) yes
checking for sys/tytchars.h... (cached) yes
checking for sys/ipc.h... (cached) yes
checking for sys/bitypes.h... (cached) yes
checking for sys/mbuf.h... (cached) no
checking for sys/sem.h... (cached) yes
checking for sys/select.h... (cached) yes
checking for sys/file.h... (cached) yes
checking for sys/ioctl.h... (cached) yes
checking for sys/fcntl.h... (cached) yes
checking for sys/filio.h... (cached) no
checking for sys/sockio.h... (cached) no
checking for sys/termios.h... (cached) yes
checking for sys/termiol.h... (cached) no
checking for termios.h... (cached) yes
checking for termio.h... (cached) yes
checking for sys/un.h... (cached) yes
checking for netinet/in_systm.h... (cached) yes
checking for net/route.h... (cached) yes
checking for machine/endian.h... (cached) no
checking for paths.h... (cached) yes
checking for nl_types.h... (cached) yes
checking whether time.h and sys/time.h may both be included... (cached) yes
checking for ANSI C header files... (cached) yes
checking for dirent.h that defines DIR... (cached) yes
checking for opendir in -ldir... (cached) no
checking for main in -lsocket... (cached) no
checking for main in -ldl... (cached) yes
checking for main in -lld... (cached) no
checking for main in -lsvld.... (cached) no
checking for setupterm in -ltermcap... (cached) no
checking for setupterm in -lcurse... (cached) yes
checking for gethostbyname in -lc... (cached) yes
checking if we can use -lnsl... (cached) no
checking for shared libc... (cached) libc.so.6
checking for shared libnsl... (cached) libnsl.so.1
checking for shared libsocket... no
checking for shared libresolv... (cached) libresolv.so.2
checking for shared libdgc... no
checking for pid_t... (cached) yes
checking for size_t... (cached) yes
checking return type of signal handlers... (cached) void
checking whether sockaddr_un has sun_len... (cached) no
checking for sig_atomic_t... (cached) yes
checking for cc_t... (cached) yes
checking for sig_t... (cached) yes
checking for getpassphrase... (cached) no
checking for sys_errlist... (cached) yes
checking for dlopen... (cached) yes
checking for shl_load... (cached) no
checking for setupterm... (cached) yes
checking for tgeterm... (cached) yes
checking for gethostbyname2... (cached) yes
checking for gethostbyname_r... (cached) yes
checking for gethostbyaddr_r... (cached) yes
checking for getpwnid_r... (cached) yes
checking for getservbyname_e_r... (cached) yes
checking for memset... (cached) yes
checking for memcpy... (cached) yes
checking for memmove... (cached) yes
checking for strchr... (cached) yes
checking for strrchr... (cached) yes
checking for strdup... (cached) yes
```

![](img/3258bbaf790525f8c4eb25fabff7844a_304_0.png)

![](img/3258bbaf790525f8c4eb25fabff7844a_304_1.png)
