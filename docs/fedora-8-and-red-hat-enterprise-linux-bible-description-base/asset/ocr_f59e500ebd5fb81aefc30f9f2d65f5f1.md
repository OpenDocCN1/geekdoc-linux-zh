If you are not sure what format a file is in, use the `file` command as follows:

```
$ file filename
```

This command tells you if it is a GNU `tar` file, `RPM`, `gzip`, or other file format. (This is a good technique if a file was renamed and lost its extension.)

If you would like to convert a software package from one of the formats described above, you can try the `alien` utility (http://freshmeat.net/projects/alien). Although alien is not considered stable enough to use with important system packages, it can be a good tool for trying out some simple software packages on your Fedora system.

# Building and installing from source code

If no binary version of the package that you want is available, or if you just want to tailor a package to your needs, you can always install the package from source code. To begin, you can get the source code (SRPM) version of any binary packages in Fedora from the Fedora software repository (see Appendix A for details). You can modify the source code and rebuild it to suit your needs.

Software packages that are not available in RPM format are typically available in the form of a tarball (a bunch of files grouped together into a single file formatted by the `tar` utility) that has been compressed (typically by the `gzip` utility). Although the exact instructions for installing an application from a source code archive vary, many packages that are in the `.bz2`, `.tar.bz2`, `.tgz`, `.gz` and `.tar` formats follow the same basic procedure.

> TIP: Before you install from source code, you will need to install a variety of software development packages. If you have the disk space, I recommend that you install all software development packages that are recommended during Fedora installation.

The following is a minimal list of C-programming software development tools:

+   * **gcc** — Contains the `gcc` (GNU C compiler) compiler.
+   * **make** — Contains the `make` command for making the binaries from Makefiles.