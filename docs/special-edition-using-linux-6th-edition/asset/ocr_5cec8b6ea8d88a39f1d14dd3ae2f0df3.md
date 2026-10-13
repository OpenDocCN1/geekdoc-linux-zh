![](bbox=[0.046, 0.073, 0.416, 0.164])

The first part of the filename is a short string that identifies the package. After the name is the version number (in this case 0.2), which identifies the version of the *software* contained in the package. This is followed by the package release number (5). It is important to distinguish between the software *version*, and the package *release*: The version number is the version of the software that is provided by the package. In the example in Figure 16.1, it is ed, version 0.2. This number is set by the original author of the software, who is often different from the person who created the package for the software. The version number reflects the status of the software. The release number refers to the version of *this package* of the software. Sometimes, even if the original software inside the package has not changed, it is necessary to repackage it. The release number indicates which instance of the package this is.

After the release number is a short string that indicates the architecture for the package. Most packages contain software that has been compiled for a particular processor or machine architecture. For example, packages with programs compiled for Intel x86 or compatible processors usually include the architecture string i386, although they can be compiled specifically for Pentium or Pentium II processors, in which case they will include the string i586 or i686, respectively. In some cases, the contents of a package are independent of any machine architecture (for example, a package that only contains icons and not executable programs). In these cases, the architecture string noarch is used. Table 16.1 shows some common architecture strings.

**TABLE 16.1 — ARCHITECTURE STRINGS IN RPM FILENAMES**

| String | Processor |
|---|---|
| noarch | Any |
| i386, i586, i686 | Intel x86, Pentium, and compatibles |
| alpha | DEC Alpha |
| sparc | Sun Sparc |
| mips | MIPS |
| ppc | PowerPC |
| m68k | Motorola 68000 family |

Often, the files required for a piece of software are bundled into a single package. Sometimes, however, the files are provided in multiple separate packages. This is done to give you additional flexibility in installing only those parts of a program that you are actually going to use. When the software's files are separated in this manner, you can often tell from the package name what kinds of files are contained in the package. Table 16.2 shows a few naming conventions that will help you to identify packages that have files for particular uses.