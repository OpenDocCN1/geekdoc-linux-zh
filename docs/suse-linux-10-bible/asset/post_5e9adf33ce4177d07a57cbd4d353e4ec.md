
## Chapter 12 ♦ Working with Packages

### Compiling RPM from the Spec File

To set up your environment for compiling the RPM, the file has to be located in /usr/src/packages/SOURCES. You need to use the rpmbuild program to take the spec file and compile the source based on the configuration you have specified. The -bb argument is used to specify that you want to build (b) and binary (b) package.

You can see in Listing 12-10 how the build process follows the spec file you have created, growing with %prep, %setup, and %files to compile a binary RPM.

### Listing 12-10: Using rpmbuild to Compile the logcheck Source

```
build: # rpmbuild -bb /tmp/logcheck.spec
Executing$(prep); /bin/sh -e /var/rpm-tmp.48125
+ umask 022
+ cd /usr/src/packages/BUILD
+ cd /usr/src/packages/BUILD
+ rm -rf logcheck-1.1.2
+ /usr/bin/gzip -dc /usr/src/packages/SOURCES/logcheck-1.1.2.tar.gz
+ tar -xf
+ STARTUP=0
+ [ $0 -ne 0 ]
+ cd logcheck-1.1.2
+ /usr/bin/id -u
+ [ $0 = 0 ]
+ /bin/chown -R root root
+ /usr/bin/id -u
+ [ $0 = 0 ]
+ /bin/chgrp -R root
+ /bin/chmod -Rf +a-X,g-w,o-w
+ exit 0
Executing$(build); /bin/sh -e /var/rpm-tmp.48125
+ umask 022
+ cd /usr/src/packages/BUILD
+ /bin/rm -rf /tmp/logcheck-buildroot
+ dirname /tmp/logcheck-buildroot
+ /bin/mkdir -p /tmp
+ cd /tmp/logcheck-buildroot
+ cd logcheck
+ make
Making logcheck
cc -O0 -o src/logtail src/logtail src/logtail.c
src/logtail.c:56: warning: return type of 'main' is not 'int'
+ exit 0
Executing$(install); /bin/sh -e /var/rpm-tmp.48125
```

### Listing 12-10 (continued)

```
+ umask 022
+ cd /usr/src/packages/BUILD
+ cd logcheck-1.1.1.2
+ rm -rf /tmp/logcheck-buildroot
+ mkdir -p /tmp/logcheck-buildroot/usr/sbin
+ mkdir -p /tmp/logcheck-buildroot/etc
+ mkdir -p /tmp/logcheck-buildroot/etc/cron.hourly
+ install /systems/linux/logcheck.hacking /tmp/logcheck-buildroot/etc/logcheck
+ install /systems/linux/logcheck.violations /tmp/logcheck-buildroot/etc/logcheck
+ install /systems/linux/logcheck.viations.ignore /tmp/logcheck-buildroot/etc/logcheck
+ install /systems/linux/logcheck.ignore /tmp/logcheck-buildroot/etc/logcheck
+ install /systems/linux/logcheck.sh /tmp/logcheck-buildroot/usr/sbin
+ install /usr/sbin/tmp/logcheck-buildroot/usr/sbin
+ cat
+ RPM_BUILD_ROOT=/tmp/logcheck-buildroot
+ export RPM_BUILD_ROOT
+ test -c /usr/sbin/check -a 0 = 0 -x /usr/sbin/check -a '1' -z /tmp/logcheck-buildroot
+ echo I /usr/sbin/Check...
I call /usr/sbin/Check
+/usr/sbin/Check
+/usr/lib/rpm/brp-components
Processing file: logcheck-1.1.2.2
Executing: /bin/sh -e /var/tmp/rpm-pm.11584
+ umask 022
+ cd /usr/src/packages/BUILD
+ cd logcheck-1.1.2
+ DOCUMENT /tmp/logcheck-buildroot/usr/share/doc/packages/logcheck
+ rm -f /tmp/logcheck-buildroot/usr/share/doc/packages/logcheck
+ /mkdir -p /tmp/logcheck-buildroot/usr/share/doc/logcheck
+ cp -p CHANGES README.keywords how.to.interpret README.keywords
systems/linux/REAME.linux systems/linux/REAME.IMPORTANT /tmp/logcheck-
buildroot/usr/share/doc/packages/logcheck
+ exit 0
Finding Providers: /usr/lib/rpm/find-provides
Finding Requirements: /usr/lib/rpm/find-requires
Requires (rpm): rpalib (Payload:LoadFilesFilePrefix) <= 4.0-1 rpalib (CompressedFileNames) <=
3.0.4-1
Requirements: cron /usr/sbin(s): /bin/sh glibc.so.6 glibc.so.6 (GLIBC 2.0) glibc.so.6 (GLIBC 2.1)
Checking for unpacked file: /usr/sbin(s): /usr/lib/rpm/check-files /tmp/logcheck-buildroot
Write: /usr/src/packages/RPMS/logcheck-1.1.2-2.1.1586.rpm
Executing: $(clean); /bin/sh -e /var/tmp/rpm-pm.1421
+ umask 022
+ cd /usr/src/packages/BUILD
+ cd logcheck-1.1.2
+ rm -rf /tmp/logcheck-buildroot
+ exit 0
```

### Checking the RPM

The RPM has been successfully created. In the next section, you check the RPM and install it.

When an RPM has been created, it is stored in /usr/src/packages/RPMS/i586. For other architectures (like x86, and so on), RPMs are saved in the relevant subdirectory. You can check the existence of the file and also list the files in the package as you did earlier in the chapter with the rpm qlp command, as shown in Listing 12-11.

### Listing 12-11: Listing the Files in the logcheck RPM

```
bible:/usr/src/packages/RPMS/i586 # rpm -qlp logcheck-
/etc/cron.hourly/logcheck
/etc/logcheck
/etc/logcheck.hacking
/etc/logcheck.ignore
/etc/logcheck.violations
/etc/logcheck.violations.ignore
/usr/sbin/logtail
/usr/share/doc/packages/logcheck/CHANGES
/usr/share/doc/packages/logcheck/CREDITS
/usr/share/doc/packages/logcheck/README
/usr/share/doc/packages/logcheck/how.to.interpret
/usr/share/doc/packages/logcheck/README.keywords
//README.IMPORTANT
```

You can see the RPM is there and looks correct based on your configuration in the spec file. You are now ready to install the RPM, as shown in Listing 12-12, with rpm -Uvh (upgrade, verbose, and show hash).

### Listing 12-12: Installing the logcheck RPM

```
bible:/usr/src/packages/RPMS/i586 # rpm -Uvh logcheck-1.1.2-2.i586.rpm
Preparing...################################ [100%]
logcheck ################################# [100%]
```

The RPM you have taken from source, created the spec file for, and compiled into a binary RPM is finally integrated into our system. RPM creation is something that the distributors have to do for every release, bug-fix, and update of a package. SUSE includes over 3,000 packages already, so the possibility of not having software that fulfills your need is quite slim. However, in the event that you't find a package, like logcheck, RPM creation is a useful skill to have.

Ultimately, knowing how an RPM is built and what RPM authors can do with an RPM package proves useful when you are working with packages themselves. It enables you to see how dependencies, post-installation scripts, and file specifications impact how your packages work installed.

## Working with Files

In a way, "Working with Files" could have been the title of the whole book. After all, just about everything you do with your system is working with files. In fact, the Unix philosophy that everything is a file, it's almost true.

In this chapter we look at some of the common tools for examining and manipulating files. We also look at working with the most common file formats and compressing and archiving files. Finally, we touch on issues surrounding file attributes and access control lists (ACLs).

### In This Chapter

- Listing, copying, and moving files
- Finding files
- Viewing files and file types
- Compressing files
- Working with archives
- Using file attributes and ACLs

### Listing, Copying, and Moving Files

We covered the fundamental concepts of listing, copying, and moving files in Chapter 2. In this section, we review those concepts and expand on them.

### The Command-Line Tools

You can list files at the command line with the `ls` command, or you can use commands as `ls -v` or `ls -m` to work with those files.

### Using ls

We doubt that many people know all of the options to the `ls` command, and we shall not list them all here. If you're curious, read the man page (`man ls`) or, better, the info pages (`info coreutils ls`). But there are a few important things about the behavior of `ls`. If you don't use the -a or -A option, you will not see the hidden files (that is, those with names starting with a dot). It can be easy to forget about this possibility — for example, consider the following:

```
user@bible:-> rmdir directory/
rmdir: directory/: Directory empty
user@bible:-> cd directory/
user@bible:-> ls
user@bible:>
user@bible:-> ls -a
.. .file
```

Here we tried to remove the directory that appeared to be empty because the ls command on its own produced no output. But -a shows that there is a hidden file in it, which is why the rmdir command failed.
