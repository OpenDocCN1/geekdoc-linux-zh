
- Reconfigure required files—RPM allows dependencies to be specified in terms of either individual files or entire RPM packages. If a dependency is given in terms of an individual file, you may be able to reconfigure your system to provide that dependency, if appropriate support exists in another file. For instance, an RPM might look for a library in a location other than the one in which it's installed on your system. In that case, creating a symbolic link from the expected location to the file's true position should allow the RPM to install normally.
- Install the required package—You can install the required RPM package to satisfy the dependency. You can either install the packages in sequence or at the same time (by specifying both on the same rpm line). If the latter, it doesn't matter in what order you list the RPM files.

Another common problem when installing RPM files is in a file conflict. If an RPM you're trying to install contains files that would overwrite files owned by another RPM, the system will refuse to install the RPM. You'll have to determine whether you want to overwrite the existing file on a case-by-case basis. If you decide to install the new RPM, you can do so by specifying the --force parameter, as in

```
rpm -Uvh filename.rpm --force
```

## Tip

Before forcing an installation over existing files, you may want to back up the existing files by renaming them or copying them to another directory. That way, if you decide to uninstall the new package, you can easily restore the original files. Similarly, if you prefer to have the original files back while still using the new RPM, you can replace the new RPM's files with the old ones.

## CAUTION

It's always wise to back up configuration files related to a program before upgrading. The RPM system contains mechanisms to do this automatically, but only if the maintainer of the RPM specifies the configuration files correctly. I've had configuration files replaced by "updated" files inappropriate for my system when upgrading RPMs.

## Creating a Binary RPM from a Source RPM

If you have a source RPM, you can install a working program by a two-step process:

- 1. Create a binary RPM from the source RPM.
- 2. Install the binary RPM as described earlier.

To perform the first step, type:

```
rpm --rebuild sourcefile.rpm
```

The rpm program then performs several operations:

- 1. Extracts the source code from sourcefile.rpm, placing a tarball in /usr/src/redhat/SOURCES and the uncompressed source code in a subdirectory of /usr/src/redhat/BUILD.
- 2. Compiles the source code.
- 3. Creates a binary RPM file in the /usr/src/redhat/RPMS/arch directory (where arch is the architecture, such as i386).
- 4. Deletes the intermediate files, leaving only the original sourcefile.rpm and the new binary RPM file.

In most cases, these steps all occur without any direct intervention on your part. When the process finishes, you can install the new binary RPM file directly, copy it to another directory and install the package from there, or even copy the RPM file to another computer and install it there.

## Note

Depending upon the size of the program and the speed of your computer, creating a binary RPM from a source RPM may take anywhere from a few seconds to quite a few minutes or even hours. During the compile process, you should see a string of compilation commands, but no progress indicator per se, so you won't know how long the process will take except by guestimating from the size of the source package—and that only after you have some experience with compiling packages on your computer.

Occasionally the creation of a binary RPM will fail. There are two common causes of such a failure:

- Missing files—If the program relies upon some package, such as Motif or LessTif libraries, and if this package isn't installed, compilation will fail. The compilation messages may provide some clue about what may be missing, but it won't be as obvious as "install the LessTif package to compile this program." Try doing a Web search on promising-sounding error messages near the end of the compiler output to find what's missing, or check the documentation for information on libraries and utilities the software requires.

- System incompatibilities—If you're trying to compile an older source RPM for a newer system, or any source RPM for an unusual architecture, you may run into incompatibilities. For instance, the older program might not compile properly with your newer C compiler. Chances are you'll need to modify the source code to get the compilation to succeed. This is a topic well beyond the scope of this book, but if you're familiar with C (or whatever language the package uses), you can take a stab at it by editing the files in the /usr/src/redhat/BUILD/packagename directory. You'll then need to either build and install the package manually (as described shortly) or create a new source RPM file, which again, is beyond the scope of this book.

Generally speaking, if you can create a binary RPM from a source RPM, you can install it and use it. Occasionally, though, the binary RPM will exhibit odd bugs or not run at all. In such a case, you'll have to debug the program as you would any other.

## Uninstalling RPMs

If you decide that you no longer need a program, you can easily uninstall it by using the -e parameter to rpm, as in

```
rpm -e packagename
```

Note that you don't specify the full filename of the package, just the package's main name. For instance, the package zsh, which I used as an example earlier for installation, comes in the file called zsh-3.0.5-10.i386.rpm. To install it, you enter the full filename, but to uninstall it, you would type

```
rpm -e zsh
```

If you're not sure of a package's name, you can try using RPM's query feature, which you initiate with the -q parameter. For instance, you could type

```
rpm -q zsh
```

If the package zsh is installed, RPM returns further details—namely, the package name and its full version number. If the package isn't installed, RPM says so. You can therefore try several variant names until you find the one that's correct.
