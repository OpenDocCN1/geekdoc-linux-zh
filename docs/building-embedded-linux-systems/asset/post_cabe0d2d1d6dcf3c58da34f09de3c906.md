
adapted to cross-compilation, and it is currently not possible to cross-compile a full Perl package.

However, two build options for cross-compiling small versions of the full Perl package do exist: microperl and miniperl. Note that both options are part of the same package, available on CPAN, and you do not need to download any other package.

## Microperl

Simon Cozens implemented the microperl build option, based on an idea by Ilya Zakharevich. It is the absolute bare minimum build of Perl, with no outside dependencies other than ANSI C and the *make* utility. Unlike the other builds, microperl does not require that you run the *Configure* script, which performs a great deal of tests on the installation machine before generating the appropriate files for the package’s build. Instead, microperl provides default configuration files with minimal settings that allow the core Perl interpreter to build properly. None of the language’s core features is missing from this interpreter. Of course, it does not support all the features of the full interpreter, but it is sufficient to run basic Perl applications. Because this code is considered “experimental,” for the moment you will need to evaluate most of microperl’s capabilities on your own.

We have successfully built a microperl for our DAQ module using the toolchain set up earlier, *uClibc*, and Perl 5.7.3. The resulting interpreter was able to adequately execute all Perl programs that did not have any outside references. It failed, however, to run programs that used any of the standard Perl modules.

To build microperl for your target, you must first download a Perl version from CPAN and extract it into the *$[PRJROOT]/[sysapps]* directory. Place the package in the *sysapps* directory, because it will run only on the target and will not be used to build any of the other software packages for your target. After extracting the package, move into its directory for the build (here, you cannot use a different build directory, as we did for the GNU toolchain, because Perl does not support this build method):

```
$ cd $[PRJROOT]/[sysapps]/perl-5.10.0
```

Since microperl is a minimal build of Perl, you do not need to configure anything. Build the package using the appropriate *Makefile* and instructing it to use the *uClibc* compiler wrapper instead of the standard *GCC* compiler:

```
$ make -f [Makefile.micro] CC=[c1386-uclibc-gcc]
```

This will generate a *microperl* binary in the package’s root directory. This binary does not require any other Perl components and can be copied directly to the */bin* directory of your target’s root filesystem, *$[PRJROOT]/[roots]*.

When dynamically linked with either *glibc* or *uClibc* and stripped, the *microperl* binary is about **1.5 MB** in size.

For more information on how microperl is built, have a look at the Makefile.micro Makefile and the uconfig.sh script. As work continues on microperl, it is expected that more documentation will become available.

## Miniperl

Miniperl is less minimalistic than microperl and provides most of what you would expect from the standard Perl interpreter. The main component it lacks is the Dyna-Loader XS module, which allows Perl subroutines to call C functions. It is therefore incapable of loading XS modules dynamically. This is a minor issue, however, given the type of system miniperl will be running on.

As with the main Perl build, miniperl requires that you run the Configure script to determine the system’s capabilities. Since the system for which Perl must be built is your target, the script requires you to specify information about how to communicate with that target: a hostname, a remote username, and a target-mapped directory. The script uses this information to run its tests on your target and generate the proper build files.

The main caveat concerning this method is that it requires a direct network link between the host and the target. In essence, if your target does not have some form of networking, you will be unable to build miniperl for it.

The installation methodology for miniperl is explained well in the INSTALL file provided with the 5.10.0 Perl package, under the “Cross-compilation” heading.

### Cross-Compiling the Impossible

As we’ve just seen with Perl, not all packages cross-compile easily. As a matter of fact, a great number of packages have not been designed to allow cross-compilation. We’ve mentioned a few of these, but certainly can’t list them all.

Besides trying to modify build scripts and using compilation tricks to force packages to compile for another architecture, sometimes the only realistic solution is to actually build the package on the target where it is supposed to run. At first, this may seem infeasible for most embedded systems because of their limited storage space. As we shall see in Chapter 9, however, it is possible to mount a system’s root filesystem on a server using NFS. By using an NFS-mounted root filesystem, the target can access as much storage space as the server allows.

In such a setup, it is therefore possible to cross-compile the GCC compiler itself for the target, and then use this compiler to natively compile any package directly on the target in exactly the same way the package’s build scripts expect to operate. Once the package has been compiled, the resulting binaries and libraries can thereafter be copied to a small root filesystem tailored for the target’s internal storage device, and used in the field like any other target application. Obviously, there is no need to package the cross-compiled GCC with the rest of the system in the field.

# Python

Guido van Rossum introduced Python to the world in 1991. It has since gathered many followers and, as with Perl, is a world of its own. If you are interested in Python, read Mark Lutz's Programming Python or his Learning Python (both O'Reilly). Python is routinely compared to Perl, because it often serves the same purposes, but because this is the subject of yet another “holy war,” we will not go any further. Instead, feel free to browse the main Python website at http://www.python.org for more information. The Python package, which includes the Python interpreter and the Python libraries, is available from that website under the terms of a composite license called the Python license, which is an approved open source license.

As with Perl, you will need a properly configured interpreter to run Python code on your target. Although the main Python distribution does not support cross-compilation, a patch by Christopher Lambacher that allows cross-compilation of Python 2.5 is available at http://whatschrisdoing.com/~lambachk/Python2.5_xc.compile.patch. A blog post by Lambacher at http://whatschrisdoing.com/blog/2006/11/06/howto-cross-compile-python-25 explains in detail how to get Python to cross-compile with this patch.

Follow the instructions, substituting the appropriate names for your target in the place of the arm-linux target used in the instructions. To follow the same project workspace organization that we established earlier, download and extract the Python package into the $[PRJROOT]/[sysapps] directory. Also, instead of building Python directly in its source directory, you can use a build-python directory, as we did with the GNU tools, because Python supports this build method. In addition, use the --prefix=$PREFIX/$TARGET/usr option instead of the values provided by the HOWTO. All the Python material will thereby be installed in the $PREFIX/$TARGET/usr directory. You can then customize this directory and copy it into the target’s root filesystem.

There are a couple of observations to make about the resulting package. First, you will not be able to build Python with diet libc; use either glibc or uCLibc. This means that glibc or uCLibc will have to be on your target’s root filesystem. When storage space on your target is limited, we recommend you use uCLibc instead of glibc.

Second, Python has installed many libraries in the $PREFIX/$TARGET/usr/lib/python2.2 directory, and many of those are large. You may want to trim down the content of this directory by deleting the components you are unlikely to use. By itself, the dynamically linked and stripped Python interpreter is 725 KB in size. Nevertheless, Python’s size and dependencies have not stopped developers from using it. A number of projects, including the OLPC’s entire “Sugar” environment, make heavy use of Python. And a growing number of major Linux distributions are now even requiring a minimal Python interpreter in order to even boot normally.

Finally, you may see some warnings and failures during the build. This is because some libraries and applications are missing from your target. The Tkinter interface to
