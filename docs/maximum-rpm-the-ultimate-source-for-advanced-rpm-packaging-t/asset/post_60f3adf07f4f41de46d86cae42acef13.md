
Chapter 16, “Making a Package That Can Build Anywhere,” has complete instructions on the modifications necessary to configure a package to use an alternate build root, as well as methods to permit users to build packages without root access. Assuming that the necessary modifications have been made, here is what the build would look like:

```bash
# rpm -ba --buildroot /tmp/foonly cdplayer-1.0.spec
* Package: cdplayer
Executing: %prep
+ cd /usr/src/redhat/BUILD
...
+ exit 0
Executing: %build
+ cd /usr/src/redhat/BUILD
+ cd cdplayer-1.0
...
+ exit 0
+ umask 022
Executing: %install
+ cd /usr/src/redhat/BUILD
+ cd cdplayer-1.0
+ make ROOT=/tmp/foonly install
install -m 755 -o 0 -g 0 -d /tmp/foonly/usr/local/bin/
install -m 755 -o 0 -g 0 cdp /tmp/foonly/usr/local/bin/
rm -f /tmp/foonly/usr/local/bin/cdplay
ln -s /tmp/foonly/usr/local/bin/cdp /tmp/foonly/usr/local/bin/cdplay
install -m 755 -o 0 -g 0 -d /tmp/foonly/usr/man/
install -m 755 -o 0 -g 0 cdp.1 /tmp/foonly/usr/local/man/man1/
+ exit 0
Executing: special doc
+ cd /usr/src/redhat/BUILD
+ cd cdplayer-1.0
+ DOCDIR=/tmp/foonly//usr/doc/cdplayer-1.0-1
+ rm -rf /tmp/foonly//usr/doc/cdplayer-1.0-1
+ mkdir -p /tmp/foonly//usr/doc/cdplayer-1.0-1
+ cp -a README /tmp/foonly//usr/doc/cdplayer-1.0-1
+ exit 0
Binary Packaging: cdplayer-1.0-1
Finding dependencies...
Requires (2): libc.so.5 libncurses.so.2.0
usr/doc/cdplayer-1.0-1
usr/doc/cdplayer-1.0-1/README
usr/local/bin/cdp
usr/local/bin/cdplay
usr/local/man/man1/cdp.1
93 blocks
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/i386/cdplayer-1.0-1.i386.rpm
+ umask 022
+ echo Executing: %clean
Executing: %clean
+ cd /usr/src/redhat/BUILD
+ cd cdplayer-1.0
+ exit 0
Source Packaging: cdplayer-1.0-1
cdplayer-1.0.spec
cdplayer-1.0.tgz
82 blocks
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/cdplayer-1.0-1.src.rpm
```

As the somewhat edited output shows, the `%prep`, `%build`, and `%install` sections are executed in RPM's normal build directory. However, the `--buildroot` option comes into play when the `make install` is done. As we can see, the `ROOT` variable is set to `/tmp/foonly`, which was the value following `--buildroot` on the command line. From that point on, we can see that `make` substituted the new build root value during the install phase.

The build root is also used when documentation files are installed. The documentation directory `cdplayer-1.0-1` is created in `/tmp/foonly/usr/doc`, and the `README` file is placed in it.

The only remaining difference that results from using `--buildroot` is that the files to be included in the binary package are not located relative to the build system's root directory. Instead, they are located relative to the build root `/tmp/foonly`. The resulting binary and source package files are functionally equivalent to packages built without the use of `--buildroot`.

### 12.1.13.1. Using --buildroot Can Bite You!

Although the `--buildroot` option can solve some problems, using a build root can actually be dangerous. How? Consider the following situation:

- A spec file is configured to have a build root of `/tmp/blather`, for instance.
- In the `%prep` section (or the `%clean` section; it doesn't matter—the end result is the same), there is an `rm -rf $RPM_BUILD_ROOT` command to clean out any old installed software.
- You decide to build the software so that it installs relative to your system's root directory, so you enter the following command: `rpm -ba --buildroot / foo.spec`.

The end result? Since specifying `/` as the build root sets `RPM_BUILD_ROOT` to `/`, that innocuous little `rm -rf $RPM_BUILD_ROOT` turns into `rm -rf /`! A recursive delete, starting at your system's root directory, might not be a total disaster if you catch it quickly, but in either case, you'll be testing your ability to restore from backup (er, you do have backups, don't you?).

The moral of this story is to be very careful when using `--buildroot`. A good rule of thumb is to always specify a unique build root. For example, instead of specifying `/tmp` as a build root (and possibly losing your system's directory for holding temporary files), use the path `/tmp/mypackage`, where the directory `mypackage` is used only by the package you're building.

### 12.1.14. `--timecheck <secs>`: Print a Warning if Files to Be Packaged Are More Than `<secs>` Old

While it’s possible to detect many errors in the `%files` list using `rpm -bi`, there is another type of problem that can’t be detected. Consider the following scenario:

- A package you’re building creates the file `/usr/bin/foo`.
- Because of a problem with the package’s makefile, `foo` is never copied into `/usr/bin`.
- An older, incompatible version of `foo`, created several months ago, already exists in `/usr/bin`.
- RPM creates the binary package file.

Is the incompatible `/usr/bin/foo` included in the package? You bet it is! If only there were some way for RPM to catch this type of problem.

Well, there is! If you add `--timecheck`, followed by a number, RPM will check each file being packaged to see if the file is more than the specified number of seconds old. If it is, a warning message is displayed. The `--timecheck` option works with either the `-ba` or `-bi` options. Here’s an example using `-bi`:

```bash
# rpm -bi --timecheck 3600 ccdplayer-1.0.spec
* Package: ccdplayer
File List Check: ccdplayer-1.0-1
warning: TIMECHECK failure: /usr/doc/ccdplayer-1.0-1/README
Finding dependencies ...
Requires (2): libc.so.5 libncurses.so.2.0
```

In this example, the file `/usr/doc/ccdplayer-1.0-1/README` is more than 3,600 seconds, or 1 hour, old. If we take a look at the file, we find that it is as follows (note that the package was built substantially later than November 1995):

```bash
# ls -al /usr/doc/ccdplayer-1.0-1/README
-rw-r--r-- 1 root root 1885 Nov 10 1995 README
```

In this case, the warning from `--timecheck` is no cause for alarm. Since the `README` file was simply copied from the original source, which was created November 10, 1995, its date is unchanged. If the file had been an executable or a library that was supposedly built recently, `--timecheck`’s warning should be taken more seriously.

If you’d like to set a default time check value of one hour, you can include the following line in your `rpmmac` file:

```text
timecheck: 3600
```

This value can still be overridden by a value on the command line, if desired. For more information on the use of `rpmmac` files, see Appendix B, “The `rpmmac` File.”

### 12.1.15. `-vv`: Display Debugging Information

Unlike most other `RPM` commands, there is no `-v` option for `rpm -b`. That’s because the command’s default is to be verbose. However, even more information can be obtained by adding `-vv`. Here’s an example:

```bash
# rpm -bp -vv cdplayer-1.0.spec
D: Switched to BASE package
D: Source(0) = sunsite.unc.edu:/pub/Linux/apps/sound/cds/cdplayer-1.0.tgz
D: Switching to part: 12
D: fileFile =
D: Switching to part: 2
D: fileFile =
D: Switching to part: 3
D: fileFile =
D: Switching to part: 4
D: fileFile =
D: Switching to part: 10
D: fileFile =
D: Switched to package: (null)
* Package: cdplayer
D: RUNNING: %prep
+ umask 022
+ echo Executing: %prep
Executing: %prep
+ cd /usr/src/redhat/BUILD
+ cd /usr/src/redhat/BUILD
+ rm -rf cdplayer-1.0
+ gzip -dc /usr/src/redhat/SOURCES/cdplayer-1.0.tgz
+ tar -xvvf -
drw rwx r-x 1 root/users 0 Aug 4 22:30 1996 cdplayer-1.0/
-rw-r--r-- root/users 17982 Nov 10 01:10 1995 cdplayer-1.0/COPYING
---
-rw-r--r-- root/users 1515 Nov 10 01:10 1995 cdplayer-1.0/volume.h
+ [ 0 -ne 0 ]
+ cd cdplayer-1.0
+ cd /usr/src/redhat/BUILD/cdplayer-1.0
+ chown -R root.root .
+ chmod -R a+rx,g-w,o-w .
+ exit 0
```

Most of the output generated by the `-vv` option is preceded by a `D:`. In this example, the additional output represents `RPM`’s internal processing during the start of the build process. Using the `-vv` option with other build commands will produce different output.

### 12.1.16. `--quiet`: Produce As Little Output As Possible

As mentioned earlier, the build command is normally verbose. The `--quiet` option can be used to cut down on the command’s output:

```bash
# rpm -ba --quiet cdplayer-1.0.spec
Package: cdplayer
```
