
```
▼
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-10.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-2.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-3.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-4.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-5.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-6.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-7.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-8.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-9.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ.html
/usr/share/doc/FAQ/html/AfterStep-FAQ/new.gif
/usr/share/doc/FAQ/html/AfterStep-FAQ/next.gif
/usr/share/doc/FAQ/html/AfterStep-FAQ/prev.gif
▲
```

![](img/5ced0c78d748bd190e9027e5549a3622_183_0.png)

![](img/5ced0c78d748bd190e9027e5549a3622_183_1.png)

> > The preceding example of the FAQ package is a great place to start, because it has no dependencies. One of the great frustrations of working with RPM is that there are inconsistencies in the dependencies listed, so an attempt to install one package often causes you to install a half dozen updated library and support packages first. It can be most frustrating!

Being able to quickly and easily install RPM packages from the Web is one of the true luxuries of working with Linux. It's just as easy to update your installed software against a newly downloaded RPM, too (use rpm -Uvh package rather than -ivh, for example). To delete a package, use rpm -e packagename. The most helpful rpm flags are summarized in Table 8.1.

## TABLE 8.1 Helpful Flags to rpm

| Flag | Meaning |
|------|---------|
| -e | Eliminate the specified RPM package from the system. |
| -h | Show progress of any downloads as hash marks (#) on the screen. |
| -i | Install. (Use with -v to see what's going on.) |
| -p | Query an uninstalled package. Quite helpful! |
| -q | Query the RPM database: -qa queries all packages, or you can specify a package by name. |
| -U | Upgrade whatever parts of the specified package have changed since the last install. |
| -v | Verbose—RPM usually only lists errors, which can be disconcerting. Use -v to see what it's doing. |

## Package Management in Darwin

There is no built-in default package manager in Darwin, and while Mac OS X has a very sophisticated installation system for Mac applications, it's not accessible from the command line, nor does it particularly help you extend the Unix side of things.

The good news is that the open source community has banded together and built a very sophisticated alternative package management system called fink.

![](img/5ced0c78d748bd190e9027e5549a3622_184_0.png)

> > Wondering what fink means? From the original developer: "Fink is the German name for Finch, a kind of bird. I was looking for a name for the project, and the name of the OS, Darwin, led me to think about Charles Darwin, the Galapagos Islands, and evolution. I remembered a piece about the so-called Darwin Finches and their beaks from school, and well, that's it...." You can read more at the great fink FAQ at http://fink.sourceforge.net/faq/.

To get started with fink, you need to download the initial fink distribution package, which is packaged as a standard Mac OS X application binary.

## Task 8.3: Installing and Working with fink

The first step toward using fink on your OS X Macintosh is to make sure that you've installed Developer Tools, which was included with your Mac OS X distribution. If you don't have it, you can always download it from Apple at http://developer.apple.com/tools/macosxtools.html.

Once you're ready, pop over to http://fink.sourceforge.net/ and click on the Downloads link. Then you'll want to choose the Binary Installer, which is a bit less than 8MB.

Once that's downloaded, click on the .pkg opened box icon to install the fink system. Remember that you'll need your administrative password for this install to succeed, as shown in Figure 8.1.

Once you've done that, it'll zip through various screens and finish up without error. There's one more step necessary: When you start up Terminal in OS X, make sure you add /sw/bin and /sw/sbin to your PATH so the commands can be found. In fact, you might also add a second environment variable while you're editing your .cshrc (or equivalent): MANPATH="/sw/share/man" to ensure that the man pages for the fink-installed applications can be found. Now you're ready to get started!

## FIGURE 8.1

Administrative password prompt.

![](img/5ced0c78d748bd190e9027e5549a3622_185_0.png)

- 1. The fink application is installed in the directory `/sw/bin`, so let's start with the list command to see what's included in the distribution:

```
# fink list | head
```

```
Reading package info...
Information about 251 packages read.
a2ps 4.12-4 Any to PostScript filter.
anacron 2.3-3 A periodic command scheduler
ant 1.4.1-2 Java based build tool.
apache 1.3.20-2 Flexible and extensible web server
app-defaults 20010814-1 Creates an app-defaults directory for fink
i apt 0.5.4-1 Advanced front-end for dpkg
audiofile 0.2.1-2 Audio File Library
autoconf 2.13-3 System for generating configure scripts
```

One significant difference between fink and RPM is that fink has an underlying network connectivity capability that lets it list all the packages that you could install, with those that you have installed delimited with the i in the left edge of the listing (see the apt package, for example).

This means that if you want to see what packages you've installed, simply feed the output of fink to a grep:

```
# fink list | grep '^i '
```

```
i apt 0.5.4-1 Advanced front-end for dpkg
i base-files 1.3-1 Directory infrastructure
i bzip2 1.0.4-4 Block-sorting file compressor
i debianutils 1.15-4 Misc. utilities specific to Debian (and Fink)
i dpkg 1.9.17-2 The Debian package manager
i fink 0.9.4-1 The Fink package manager
i gettext 0.10.40-1 Message Localization support
i gzip 1.2.4a-5 The gzip file compressor
i libiconv 1.7-3 Character set conversion library
i ncurses 5.2-5 Full-screen ascii drawing library
i tar 1.13.19-1 GNU tar - tape archiver
```

Packages that might have (i) as their status are installed, but there's a newer version available.

- 2. Now that we have fink installed, we can remedy a couple of problems with the Darwin distribution. It's time to install bash, a command shell that is the first choice of many Unix sysadmins.

```
# fink install bash
Reading package info...
Information about 288 packages read in 1 seconds.
pkg bash version ###
pkg bash version 2.05-3
The following package will be installed or updated:
bash
The following 2 additional packages will be installed:
dlcompat readline
Do you want to continue? [Y/n] y
curl -L -O http://ftp.gnu.org/gnu/bash/bash-2.05.tar.gz
curl -L -O http://prdownloads.sourceforge.net/fink/dlcompat-20010831.tar.gz
curl -L -O http://ftp.gnu.org/gnu/readline/readline-4.2.tar.gz
mkdir -p /sw/src/dlcompat-20010831
tar xvfz /sw/src/dlcompat-20010831.tar.gz
dlcompat-20010831/
dlcompat-20010831/APPLE_LICENSE
dlcompat-20010831/ChangeLog
dlcompat-20010831/dlfcn.h
dlcompat-20010831/dlopen.c
dlcompat-20010831/Makefile
dlcompat-20010831/README
make prefix=/sw
cc -Wall -O2 -DDEBUG=0 -fno-common -o dlopen.o -c dlopen.c
... lots and lots of output removed ...
mkdir -p /sw/fink/dists/stable/main/binary-darwin-powerpc/shells
dpkg -b root-bash-2.05-3
/sw/fink/dists/stable/main/binary-darwin-powerpc/shells
dpkg-deb: building package 'bash' in
'/sw/fink/dists/stable/main/binary-darwin-powerpc/shells/bash_2.05-3_darwin-powerpc.deb'.
ln -sf
/sw/fink/dists/stable/main/binary-darwin-powerpc/shells/bash_2.05-3_darwin-powerpc.deb
/sw/fink/debs/
rm -rf /sw/src/root-bash-2.05-3
dpkg -i
/sw/fink/dists/stable/main/binary-darwin-powerpc/shells/bash_2.05-3_darwin-powerpc.deb
Selecting previously deselected package bash.
(Reading database ... 3476 files and directories currently installed.)
Unpacking bash (from .../bash_2.05-3_darwin-powerpc.deb) ...
Setting up bash (2.05-3) ...
* Bash: (bash) The GNU Bourne-Again SHell.
install-info: no section specified for new entry, placing at end
```
