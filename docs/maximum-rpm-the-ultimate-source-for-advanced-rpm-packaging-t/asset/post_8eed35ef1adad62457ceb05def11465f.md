
## 20.3.2.2. Adding `%files` Lists

The last part of our initial attempt at a spec file is a `%files` list for each package the spec file will build. Because we're planning on a client and a server subpackage, we'll need two `%files` lists. For the time being, we'll just add the `%files` lines; we'll be adding the actual filenames later:

```
%files client

%files server
```

There's certainly more to come, but this is enough to get us started. And the first thing we want RPM to do is to unpack the amanda sources.

### 20.3.3. Getting the Original Sources Unpacked

In keeping with a step-by-step approach, RPM has an option that let's us stop the build process after the `%prep` script has run. Let's give the `-bp` option a try and see how things look:

```
# rpm -bp amanda-2.3.0.spec
* Package: amanda
* Package: amanda-client
* Package: amanda-server
+ umask 022
+ echo Executing: '%prep'
Executing: '%prep'
+ cd /usr/src/redhat/BUILD
+ cd /usr/src/redhat/BUILD
+ rm -rf amanda-2.3.0
+ gzip -dc /usr/src/redhat/SOURCES/amanda-2.3.0.tar.gz
+ tar -xvf -
drwxr-xr-x   3/20       0 May 19 22:10 1996 amanda-2.3.0/
-rw-r-r--   3/20      1389 May 19 22:11 1996 amanda-2.3.0/COPYRIGHT
-rw-r-r--   3/20      1958 May 19 22:11 1996 amanda-2.3.0/Makefile
-rw-r-r--   3/20     11036 May 19 22:11 1996 amanda-2.3.0/README
...
-rw-r-r--   3/20      2010 May 19 22:11 1996 amanda-2.3.0/man/amtape.8
drwxr-xr-x   3/20       0 May 19 22:11 1996 amanda-2.3.0/tools/
drwxr-xr-x   3/20      2437 May 19 22:11 1996 amanda-2.3.0/tools/munge
+ [ 0 -ne 0 ]
+ cd amanda-2.3.0
+ cd /usr/src/redhat/BUILD/amanda-2.3.0
+ chown -R root.root .
+ chmod -R a+rX,g-w,o-w .
+ exit 0
#
```

By looking at the output, it would be pretty hard to miss the fact that the sources were unpacked. If we look in RPM's default build area (`/usr/src/redhat/BUILD`), we'll see an amanda directory tree:

```
# cd /usr/src/redhat/BUILD/
# ls -l
total 3
drwxr-xr-x 11 root root 1024 May 19 1996 amanda-2.3.0
#
```

After a quick look around, it seems like the sources were unpacked properly. But wait—where are our carefully crafted configuration files in `config`? Why isn't `tools/munge` modified?

### 20.3.4. Getting Patches Properly Applied

Ah, perhaps our `%prep` script was a bit too simple. We need to apply our patch. So let's add two things to our spec file:

- A `%patch` tag line pointing to our patch file
- A `%patch` macro in our `%prep` script

Easy enough. At the top of the spec file, along with the other tags, let's add

```
Patch: amanda-2.3.0-1inux.patch
```

Then we'll make our `%prep` script look like this:

```
%prep
%setup
%patch -p 1
```

There, that should do it. Let's give that `-bp` option another try:

```
# rpm -bp amanda-2.3.0.spec
* Package: amanda
* Package: amanda-client
* Package: amanda-server
+ umask 022
+ echo Executing: %prep
Executing: %prep
+ cd /usr/src/redhat/BUILD
+ cd /usr/src/redhat/BUILD
+ rm -rf amanda-2.3.0
+ gzip -dc /usr/src/redhat/SOURCES/amanda-2.3.0.tar.gz
+ tar -xvzf -
drwxr-xr-x 3/20 0 May 19 22:10 1996 amanda-2.3.0/
-rw-r--r-- 3/20 1389 May 19 22:11 1996 amanda-2.3.0/COPYRIGHT
-rw-r--r-- 3/20 1958 May 19 22:11 1996 amanda-2.3.0/Makefile
-rw-r--r-- 3/20 11036 May 19 22:11 1996 amanda-2.3.0/README
...
-rw-r--r-- 3/20 2010 May 19 22:11 1996 amanda-2.3.0/man/amtape.8
drwxr-xr-x 3/20 0 May 19 22:11 1996 amanda-2.3.0/tools/
-rwxr-xr-x 3/20 2437 May 19 22:11 1996 amanda-2.3.0/tools/munge
+ [ 0 -ne 0 ]
+ cd amanda-2.3.0
+ cd /usr/src/redhat/BUILD/amanda-2.3.0
+ chown -R root.root .
+ chmod -R a+rX,g-w,o-w .
+ echo Patch #0:
Patch #0:
+ patch -p1 -s
+ exit 0
```

Not much difference, until the very end, where we see the patch being applied. Let's take a look into the build area and see if our configuration files are there:

```
# cd /usr/src/redhat/BUILD/amanda-2.3.0/config
# ls -l
total 58
-rw-r--r--   1 root  root   7518 May 19 1996 config-common.h
-rw-r-r--r--   1 root  root  1846 Nov 20 20:46 config.h
-rw-r-r--r--   1 root  root  2081 May 19 1996 config.h.orig
-rw-r-r--r--   1 root  root  1690 May 19 1996 config.h-basdi1
...
-rw-r--r--   1 root  root  1830 May 19 1996 config.h-ultrix4
-rw-r-r--r--   1 root  root     0 Nov 20 20:46 config.h.orig
-rw-r-r--r--   1 root  root  7196 Nov 20 20:46 options.h
-rw-r-r--r--   1 root  root  7236 May 19 1996 options.h.vanilla
-rw-r-r--r--   1 root  root     0 Nov 20 20:46 options.h.orig
#
```

Much better. Those zero-length .orig files are a dead giveaway that patch has been here, as are the dates on config.h and options.h. In the tools directory, munge has been modified, too. These sources are ready for building!

### 20.3.5. Letting RPM Do the Building

We know that the sources are ready. We know that the %build script is ready. There shouldn't be much in the way of surprises if we let RPM build amanda. Let's use the -bc option to stop things after the %build script completes:

```
# rpm -bc amanda-2.3.0.spec
* Package: amanda
* Package: amanda-client
* Package: amanda-server
...
echo Executing: %build
Executing: %build
+ cd /usr/src/redhat/BUILD
+ cd amanda-2.3.0
+ make
Making all in common-src
make[1]: Entering directory '/usr/src/redhat/BUILD/amanda-2.3.0/common-src'
../tools/munge Makefile.in Makefile.out
make[2]: Entering directory '/usr/src/redhat/BUILD/amanda-2.3.0/common-src'
cc -g -I. -I../config -c error.c -o error.o
cc -g -I. -I../config -c alloc.c -o alloc.o
...
Making all in man
make[1]: Entering directory '/usr/src/redhat/BUILD/amanda-2.3.0/man'
../tools/munge Makefile.in Makefile.out
make[2]: Entering directory '/usr/src/redhat/BUILD/amanda-2.3.0/man'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/usr/src/redhat/BUILD/amanda-2.3.0/man'
make[1]: Leaving directory '/usr/src/redhat/BUILD/amanda-2.3.0/man'
+ exit 0
#
```

As we thought, no surprises. A quick look through the build area shows a full assortment of binaries, all ready to be installed. So it seems that the most natural thing to do next would be to let RPM install amanda.

### 20.3.6. Letting RPM Do the Installing

And that's just what we're going to do! Our `%install` script has the necessary `make install` command, so let's give it a shot:

```
# rpm -bi amanda-2.3.0.spec
* Package: amanda
* Package: amanda-client
* Package: amanda-server
...
echo Executing: %build
Executing: %build
+ cd /usr/src/redhat/BUILD
+ cd amanda-2.3.0
+ make
Making all in common-src
make[1]: Entering directory '/usr/src/redhat/BUILD/amanda-2.3.0/common-src'
../tools/munge Makefile.in Makefile.out
make[2]: Entering directory '/usr/src/redhat/BUILD/amanda-2.3.0/common-src'
cc -g -I. -I../config -c error.c -o error.o
cc -g -I. -I../config -c alloc.c -o alloc.o
...
+ umask 022
+ echo Executing: %install
Executing: %install
+ cd /usr/src/redhat/BUILD
+ cd amanda-2.3.0
+ make install
Making install in common-src
make[1]: Entering directory '/usr/src/redhat/BUILD/amanda-2.3.0/common-src'
...
install -c -o bin amrestore.8 /usr/man/man8
install -c -o bin amtape.8 /usr/man/man8
make[2]: Leaving directory '/usr/src/redhat/BUILD/amanda-2.3.0/man'
make[1]: Leaving directory '/usr/src/redhat/BUILD/amanda-2.3.0/man'
+ exit 0
+ umask 022
+ echo Executing: special doc
Executing: special doc
+ cd /usr/src/redhat/BUILD
+ cd amanda-2.3.0
+ DOCDIR=/usr/doc/amanda-2.3.0-1
+ DOCDIR=/usr/doc/amanda-client-2.3.0-1
+ DOCDIR=/usr/doc/amanda-server-2.3.0-1
+ exit 0
```

Everything looks pretty good. At this point, the amanda software, built by RPM, has been installed on the build system. Since we performed all the configuration steps before, when we were manually building amanda, everything should still be configured properly to test this new build. (Of course, if the process of installing the software changed some necessary config files, they would have to be redone, but in this case it didn’t happen.) So why don’t we give the new binaries a try?

### 20.3.7. Testing RPM’s Handiwork

After a quick double-check to ensure that all the configuration steps were still in place from our manual build, we reran our tests. No problems were found. It’s time to build some packages!

## 20.4. Package Building

Okay, let’s go for broke and tell RPM to do the works, including the creation of the binary and source packages:

```
# rpm -ba amanda-2.3.0.spec
* Package: amanda
* Package: amanda-client
* Package: amanda-server
...
+ echo Executing: %build
Executing: %build
+ cd /usr/src/redhat/BUILD
+ cd amanda-2.3.0
+ make
Making all in common-src
...
+ echo Executing: %install
Executing: %install
+ cd /usr/src/redhat/BUILD
+ cd amanda-2.3.0
+ make install
Making install in common-src
...
+ echo Executing: special doc
Executing: special doc
...
Binary Packaging: amanda-client-2.3.0-1
```
