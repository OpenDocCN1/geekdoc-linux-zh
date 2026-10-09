The following example assumes you have downloaded the GNU **which** program (ftp.gnu.org/pub/gnu/which; page 255) to the working directory. First unpack and decompress the file and **cd** to the new directory:

```
$ tar -xzvf which-2.20.tar.gz
which-2.20/
which-2.20/EXAMPLES
which-2.20/posixstat.h
...
which-2.20/configure.ac
which-2.20/COPYING
$ cd which-2.20
```

After reading the README and INSTALL files and installing the gcc package, run the configure script, which gathers information about the local system and generates the Makefile file:

```
$ ./configure
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking whether to enable maintainer-specific portions of Makefiles... no
...
config.status: creating Makefile
config.status: creating maintMakefile
config.status: creating tidle/Makefile
config.status: creating config.h
config.status: executing defPlex commands
```

Refer to the **configure** info page, specifically the **--prefix** option, which causes the install phase to place the software in a directory other than **/usr/local**. For package-specific options enter the command **configure --help**. Next, run **make**:

```
$ make
make all-recursive
make[1]: Entering directory `/home/sam/which-2.20'
Making all in tidle
make[2]: Entering directory `/home/sam/which-2.20/tidle'
source='tidle.c' object='tidle.o' libtool=no \
DEPDIR=.deps depmode=pgcc /bin/bash ../depcomp \
pgcc -DWARN_CONFIG_H -I-... -g -O2 -c tiddle.c
source='shell.c' object='shell.o' libtool=no \
DEPDIR=.deps depmode=pgcc /bin/bash .../depcomp shell.c
pgcc -DWARN_CONFIG_H -I-... -g -O2 -c shell.c
rm -f libtidle.a
ar cru libtidle.a tiddle.o shell.o
...
source='which.c' object='which.o' libtool=no \
DEPDIR=.deps depmode=pgcc /bin/bash .../depcomp \
gcc -DWARN_CONFIG_H -I... -g -O2 -c which.c
gcc -g -O2 -o which getopt.o getopt1.o bash.o which.o ../tidle/libtidle.a
make[2]: Leaving directory `/home/sam/which-2.20'
make[1]: Leaving directory `/home/sam/which-2.20'
$ ls which
which
```