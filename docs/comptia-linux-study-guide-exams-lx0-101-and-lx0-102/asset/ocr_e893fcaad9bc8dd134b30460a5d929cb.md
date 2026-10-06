# Using RPM

RPM is a cross-platform tool. As noted earlier, some non-Linux Unix systems can use RPM, although most don't use it as their primary package-distribution system. RPM supports any CPU architecture. Red Hat Linux is available for at least five CPUs: x86, x86-64 (aka AMD64, EM64, and x64), IA-64, Alpha, and SPARC. Of the mentioned earlier, Yellow Dog is a PowerPC distribution (it runs on Apple PowerPC-based Macs and some non-Apple systems), and SUSE is available on x86, x86-64, and PowerPC systems. For the most part, source RPMs are transportable across architectures—you can use the same source to build packages for x86, AMD64, PowerPC, Alpha, SPARC, or any other platform you like. Some programs are composed of architecture-independent scripts and so no recompilation. There are also documentation and configuration packages that work on any CPU.

The convention for naming RPM packages is as follows:

```
packagename-a.b.c-x.arch.rpm
```

Each of the filenames has a specific meaning:

**Package Name** The first component (packagename) is the name of the package, such as as or samba-the Samba file and print server. Note that the same program may have different names by distribution managers.

**Version Number** The second component (a.b.c) is the version number, such as 3.6.5. The version number doesn't have to be period-separated numbers, but that's the most common format. The program assigns the version number.

**Build Number** The number following the version number (x) is the build number (also known as the maintainer). This represents minor changes made by the package maintainer, not by the program. These changes may represent altered startup scripts or configuration files, changed locations, added documentation, or patches attached to the original program to fix bugs or to make the program more compatible with the Linux distribution. Many distribution managers add a letter to the code to distinguish their packages from others. Note that these numbers are not comparable across package managers—George's build 5 of a package is not an improvement on Susan's build 4 of the same package.

**Architecture** The final component preceding the .rpm extension (arch) is the package's architecture. The i86 code is common; it represents a file compiled for any CPU from the 8038 origin. Some packages include optimizations for Pentiums or newer (1586 or 1686), and non-x86 binary packages use codes for their CPUs, as ppc for PowerPC CPUs or x86-64 for. Scripts, documentation, and other CPU-independent packages generally use the noarch architecture code. The main exception to this rule is source RPMs, which use the src architecture code.

As an example of RPM versioning, the Fedora 17 distribution for x86-64 chips with a Samba package called samba3.6.5-fed17.1.x86_64.rpm, indicating that this is build 86.fc17.1 of Samba 3.6.5, compiled with x86-64 optimizations. These naming