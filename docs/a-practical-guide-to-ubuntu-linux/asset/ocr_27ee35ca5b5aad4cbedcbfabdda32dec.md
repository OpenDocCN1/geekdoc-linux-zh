predictable a manner as possible. The standard Linux file structure has a hierarchy under /usr/local for binaries (/usr/local/bin), manual pages (/usr/local/main), and so forth. Many GNU buildtools search the /usr/local hierarchy by default and find the wrong version of a utility if you install developer tools, putting these tools in /opt is a good idea.

To prevent confusion later and avoid overwriting or losing the software when you install standard software upgrades, installing nonstandard software in standard system directories like /usr/bin. On a multiuser system, make sure users know where to find the local software and advise them whenever you install, change, or remove local tools.

# GNU CONFIGURE AND BUILD SYSTEM

The Configure and Build System makes it easy to build a program that is distributed as source code (see www.gnu.org/software/autoconf). This process requires requires a shell, make, and gcc (the GNU C compiler). You do not need to work with root privileges to install the program.

The following example assumes you have downloaded the GNU program (ftp.gnu.org/pub/gnu/which; page 178) to the working directory. First unpack and decompress the file and cd to the new directory:

```
$ tar -xvzf which-2.20.tar.gz
which-2.20/
which-2.20/EXAMPLES
which-2.20/posixstat.h

which-2.20/configure.ac
which-2.20/COPYING

cd which-2.20
```

After reading the README and INSTALL files, run the configure script, which gathers information about the local system and generates the Makefile:

```
$ ./configure
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /bin/mkdir -p
checking for gcc... awk
checking whether make makes $(MAKE)... yes
checking whether to enable maintainer-specific portions of Makefiles... no

config.status: creating Makefile
config.status: creating Makefile
config.status: creating tilde/Makefile
config.status: creating config.h
config.status: executing depfiles commands
```

Refer to the configure info page, specifically the --prefix option, which causes the install phase to place the software in a directory other than /usr/local. Next, run make: