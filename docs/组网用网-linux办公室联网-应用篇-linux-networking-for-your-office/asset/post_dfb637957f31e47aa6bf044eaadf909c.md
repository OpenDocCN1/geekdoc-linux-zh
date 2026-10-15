
Most mainstream Linux distributions use the RPM format for their files. Debian, of course, uses the Debian format. Slackware uses tarballs. A few others, like Stampede, use assorted other formats. You can install the package managers for a foreign distribution on any system. For instance, you can install the RPM utilities on a Slackware system, or the Debian utilities on a Red Hat system. It’s best to stick with one package format per computer, though, to avoid conflicts.

> NOTE
> 
> Because RPM is used so widely, my comments on it apply to non-Red Hat distributions that use RPM, such as Mandrake and SuSE, as well as to Red Hat itself.

## Understanding the RPM Database

The RPM utilities maintain a database of packages you’ve installed in the directory /var/lib/rpm. The files in this directory have .rpm extensions, but they aren’t RPM package files; rather, they’re databases that maintain information on installed packages, such as

- Names—The names of the packages that you have installed, such as glibc and samba.
- Versions—The version number associated with each installed package, such as 2.1.1-6 for glibc. The version number includes both the software version (2.1.1) and a build number (6). The build number refers to minor changes to the package implemented at compile time. A revised build might add or delete support files, change the location in which a file is installed, or apply a patch that’s not part of the official software release.
- Installed package dependencies—Most packages depend on one or more others for proper functioning. For instance, most programs link against the standard C libraries, which are contained in the glibc package. Therefore, most packages depend upon glibc. Sometimes a package depends upon a specific version of another package; for instance, a package might depend upon glibc 2.1 or later. The RPM system allows searching for dependencies in reverse, too. For instance, if you were to try to remove glibc, the system would refuse on the grounds that so many additional packages depend upon glibc.
- Descriptions—Each package has assorted descriptive information associated with it, including the system on which the RPM file was created, copyright and distribution terms, and an English description of what the package does.
- Included files—RPM maintains a list of files that are associated with each package. RPM can use this information to delete old files when you update or remove a package. You can also search the database to find out what package owns a specific file.

You don’t access the RPM database files directly; instead, you use the rpm program, or a GUI front-end such as gnorpm, to do the job. I describe these tools shortly.

## Source, Binary, and Noarch RPMs

RPM files come in three basic forms: source, binary, and noarch:

- Source—Source RPMs usually contain the string src as part of their filenames, as in icewm-0.9.33-1.src.rpm. Source RPMs contain source code that you can use to compile the program on your system. Normally you don’t need to use source RPMs, but they can be convenient in some cases, as when you want to recompile a program to take better advantage of some new system utility, or when you want to compile the same program for Linux running on computers with different architectures, such as Intel and PowerPC computers.
- Binary—Binary RPMs contain precompiled program code. For Intel-architecture machines, binary RPM filenames generally contain the string i386, or possibly a higher x86 value, such as i686, if the program was compiled to take advantage of more sophisticated CPUs’ features. Binary RPMs also exist for non-Intel architectures, such as PowerPC, and in such cases they have different CPU codes as part of their filenames, such as ppc. You cannot use a binary RPM for an architecture other than the one you’re using. You can often recompile a source RPM when all you can find are the source RPM and a binary for an architecture you’re not using, though.
- Noarch—Noarch stands for no architecture. A noarch RPM is one that contains information that doesn’t depend upon the architecture. RPMs for Linux documentation are noarch, for instance, as are RPMs that contain only interpreted programs like Perl scripts.

In general, it’s easiest to install binary and noarch RPMs. If you can only find a source RPM, though, you can use it to create an appropriate binary RPM and install that. If you can’t find an appropriate RPM of any form, it’s possible to create an RPM from raw source code, but doing so is beyond the scope of this book. It’s generally easier to install a program directly from the source tarball than to create an RPM from the source tarball, but you might want to create an RPM in order to maintain as much information about your system as possible in the RPM database files. This way, you can check the validity of the installed files quite easily, and you can be sure that your program won’t overwrite other programs’ files, or be overwritten by future installations. You can also more easily uninstall a program in the future if you install it from an RPM.
