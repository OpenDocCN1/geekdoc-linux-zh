+   * **glibc** — Contains important shared libraries, the C library, and the standard math library.
+   * **glibc-devel** — Contains standard header files needed to create executables.
+   * **binutils** — Contains utilities needed to compile programs (such as the assembler and linker).
+   * **kernel-devel** — Contains the Linux kernel source code and is needed to rebuild the kernel.
+   * **rpmbuild** — Contains the rpmbuild utility for building the RPM binary package from source code.
+   * **libc** — Contains libraries needed for programs that were based on `libc5`, so older applications can run on `glibc` (libc6) systems.

# Installing software in SRPM format

To install a source package from the Fedora source directory, do the following:

+   1. Refer to Appendix A for information on obtaining Fedora source code.
+   2. Download the package you want to the current directory.
+   3. Install the source code package using the following command:
+   ```bash
+   # rpm -iv *.src.rpm
+   ```
+   (Replace *packagename* with the name of the package you are installing.) The source is installed in the Fedora source tree (`/usr/src/redhat/SOURCES`). Spec files are copied to `/usr/src/redhat/SPECS`.
+   4. Change to the SPECS directory as follows:
+   ```bash
+   # cd /usr/src/redhat/SPECS
+   ```
+   5. Unpack the source code as follows:
+   ```bash
+   # rpmbuild -bp packagename*.spec
+   ```
+   6. The package’s source code is installed to the `/usr/src/redhat/BUILD/package` directory, where *package* is the name of the software package.
+   7. You can now make changes to the files in the package’s BUILD directory. Read the README, Makefile, and other documentation files for details on how to build the individual package.

The `--rebuild` option to `rpmbuild` can be used to rebuild the rpm without installing it first. The resulting binary will be in `/usr/src/redhat/RPMS/arch`, where *arch* is replaced by i386 or other architecture for which you are building the RPM.