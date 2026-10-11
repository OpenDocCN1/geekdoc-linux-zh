
require special tools other than a shell, make, and gcc (the GNU C compiler). You do not need to work with root privileges for either of these steps.

The following example assumes you have downloaded the GNU chess program (www.gnu.org/software/chess/chess.html) to the working directory. First unpack and decompress the file and cd to the new directory:

```bash
$ tar -xvzf gnuchess*
gnuchess-5.03/
gnuchess-5.03/book/
gnuchess-5.03/book/README
...
$ cd gnuchess*
```

After reading the README and INSTALL files, run the configure script, which gathers information about the local system and generates the Makefile file:

```bash
$ ./configure
checking for a BSD compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for mmap... mmap
checking whether make sets ${MAKE}... yes
checking for gcc... gcc
checking for C compiler default output... a.out
checking whether the C compiler works... yes
...
checking for memstat... yes
configure: creating ./config.status
config.status: creating Makefile
config.status: creating src/Makefile
config.status: creating src/config.h
```

Refer to the configure info page, specifically the --prefix option, which causes the install phase to place the software in a directory other than /usr/local. The second step is to run make:

```bash
$ make
Making all in src
make[1]: Entering directory '/hdd4/gnuchess-5.03/src'
cd ..\
&& CONFIG_FILES= CONFIG_HEADERS=src/config.h \
/bin/sh ./config.status
config.status: creating src/config.h
config.status: src/config.h is unchanged
make  all-am
make[2]: Entering directory '/hdd4/gnuchess-5.03/src'
source='atak.c'  object='atak.o'  libtool=no
dep='deps/atak.Po'  tmpdepfile='.deps/atak.Po'
depcompose=gcc3 /bin/sh ./depcomp \
&& -DHAVE_CONFIG_H -I . -I.. -I.\
gcc -g -O2 -o gnuchess  atak.o book.o cmd.o epd.o eval.o genmove.o hash.o hung.o init.o iterate.o main.o move.o null.o output.o players.o pgn.o queesc.o random.o repeat.o search.o solve.o sort.o swap.o test.o ttable.o util.o version.o -Lreadonly -lncurses -lm
make[2]: Leaving directory '/hdd4/gnuchess-5.03/src'
make[1]: Leaving directory '/hdd4/gnuchess-5.03/src'
make[1]: Entering directory '/hdd4/gnuchess-5.03'
make[1]: Nothing to be done for 'all-am'.
make[1]: Leaving directory '/hdd4/gnuchess-5.03'
```

```bash
$ ls src/gnuchess
src/gnuchess
```

After make finishes, the gnuchess executable is found in the src directory. If you want to install it, give the following command while running with root privileges:

```bash
# make install
Making install in src
make[1]: Entering directory '/hdd4/gnuchess-5.03/src'
make[2]: Entering directory '/hdd4/gnuchess-5.03/src'
/bin/sh ../mkinstalldirs /usr/local/bin
/usr/bin/install -c gnuchess /usr/local/bin/gnuchess
make[2]: Nothing to be done for 'install-data-am'.
...
```

You can run the two steps and install the software with this command:

```bash
# ./configure && make && make install
```

The Boolean AND operator, &&, allows the execution of the second step only if the first step returns a successful exit status.

## KEEPING SOFTWARE UP-TO-DATE

Of the many reasons to keep software up-to-date, one of the most important is security. Although you may hear about software-based security breaches after the fact, you rarely hear about the fixes that were available but never installed before the breach occurred. Timely installation of software updates is critical to maintaining system security. Linux open-source software is the ideal environment in which to find and fix bugs and make repaired software available quickly. When you keep the system and application software up-to-date, you keep abreast of bug fixes, new features, support for new hardware, speed enhancements, and more.

### Bugs

A *bug* is an unwanted and unintended program property, especially one that causes the program to malfunction (definition courtesy of www.foldoc.org). Bugs have been around forever, in many types of systems, machinery,.

## rhnsd: The RHN Daemon

The RHN daemon (rhnsd) is a background service that periodically queries the RHN server to determine whether any new packages are available to be downloaded. This daemon is one of the keys to RHN security: It initiates contact with the RHN server so the server never has to initiate contact with the local system. Refer to “service: Configures Services I” on page 427 for information on how to start, stop, or display the status of rhnsd immediately; refer to “system-config-services: Configures Services II” on page 428 or “chkconfig: Configures Services III” on page 429 for information on how to start or stop rhnsd at specified runlevels.

## wget: Downloads Files Noninteractively

The wget utility is a noninteractive, command-line utility that can retrieve files from the Web using HTTP, HTTPS, or FTP. The following simple example uses wget to download Red Hat’s home page, named index.html, to a file with the same name:

```bash
$ wget http://www.redhat.com
--2009-10-16 12:14:24--  http://www.redhat.com/
Resolving www.redhat.com... 96.6.224.112
Connecting to www.redhat.com[96.6.224.112]:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 20053 (20K) [text/html]
Saving to: ‘index.html’

100%[===============================>] 20,053        --.-K/s   in 0.008s

2009-10-16 12:14:24 (2.28 MB/s) - ‘index.html’ saved [20053/20053]
```

Use the -b option to run wget in the background and redirect its standard error to a file named wget-log:

```bash
$ wget -b http://example.com/big_file.tar.gz
Continuing in background, pid 10752.
Output will be written to ‘wget-log’ .
```

If you download a file that would overwrite a local file, wget appends a period followed by a number to the filename. Subsequent background downloads are then logged to wget-log.1, wget-log.2, and so on.
