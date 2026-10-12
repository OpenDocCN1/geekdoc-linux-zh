
## Yum

Some developers believe that although apt is a good tool, using it for .rpm packages is a hack. apt also is believed to be bloated with unnecessary code used for the Debian .deb packages. A new tool, Yum, was developed using the Python language because the Fedora Core installer, Anaconda, was written in Python and much of the code could be shared. This decision is what has made Yum the choice for integration into the Fedora Core distribution. It works much the same as apt, but lacked a GUI tool. The Fedora developers have integrated support for Yum into the graphical Red Hat/Fedora package management tool. You can obtain Yum from the Fedora site as well as from FreshRPMs.net; the home page of Yum is at http://linux.duke.edu/projects/yum/.

Here’s how you install and configure Yum:

- Read the HOWTO and Users’ FAQ at the Fedora site: http://fedora.mplug.org/.
- Install the Fedora GPG key:
  ```text
  # lynx -source http://fedora.mplug.org/FEDORA-GPG-KEY | gpg --import
  ```
- Install the correct version of Yum:
  ```text
  # rpm -ivh http://ftp.freshrpms.net/pub/freshrpms/fedora/linux/2/yum/ \
  yum-2.0.7-3.1.fc.fr.noarch.rpm
  ```
- Review the man page for Yum to familiarize yourself with all available options:
  ```text
  # man yum
  ```

Once Yum is installed, the following commands are useful (remember that the Fedora graphical client is available if you configure it to use Yum repositories):

- yum list—A list of all packages available from the repository.
- yum list installed—A list of all packages installed on your computer.
- yum list updates—A list of all updates available for your computer.
- yum install package name—Installs package name.
- yum update—Run without a package name, Yum will update all installed packages.
- yum remove package name—Removes a package and dependencies.
- yum upgrade—Run without a package name, Yum will upgrade all packages and remove any obsoleted packages; yum update will not remove obsoleted packages.

You’ll find either apt or Yum to be useful additions to Fedora Core. We suggest that you use the one from FreshRPMs.net if you want to install some of the multimedia applications described in Chapter 10, “Multimedia Applications.” To learn more about yum, check out Chapter 36, “Advanced Yum.”

### Compiling Software from Source

Not all the software you might want to use is available in rpm packages or in the exact form that you desire. Many complicated programs have options that can only be selected at compile time and many smaller, special-purpose applications only exist as source code. Fedora Core provides all the tools necessary for you to compile source code into binary applications. First, we’ll cover building from source rpm files, and then manipulating source rpm files and finally, building from source tarballs.

> **NOTE**
> For other software package formats, you can use the File Roller application (found in the Accessories menu) to easily display, browse, read, and extract contents of compressed files, including legacy archives such as tarballs or compressed tar archives (recognized by their .gz or .tgz extensions). Other compressed files, such as those created with the compress command (ending in .Z) or bzip2 files (ending in .bz2), are also supported by File Roller. The File Roller client will also convert compressed archives between gzip and bzip2 formats.

### Building RPMs from src.rpm Files

A rule of thumb is that you never build rpms as the root user even though the directories are already set up at /usr/src/redhat as follows:

```text
# tree /usr/src/redhat
/usr/src/redhat
|-- BUILD
`-- RPMs
    |-- athlon
    |-- i386
    |-- i486
    |-- i586
    |-- i686
    `-- noarch
`-- SOURCES
`-- SPECS
`-- SRPMS
```

Using the mkdir command, re-create this directory tree structure in your home directory; you can name the new directory redhat (or anything you like). You might even want to create a new user just to build rpms and source code. (You can compile without being root; you just can't install the software systemwide as a regular user.)

The configuration information for building rpms is kept in three places:

- /usr/lib/rpm/*/macros—The systemwide defaults.
- /etc/rpm/macros.*—Where systemwide changes are kept.
- ~/.rpmmacros—Where user-specific changes are kept.

Because we need to tell rpm that we will not be using the systemwide default build location for our user, we can

```text
$ echo "%_topdir $HOME/redhat" > $HOME/.rpmmacros
```

> **TIP**
> 
> Here, we use > instead of >> to blank the file in case there is already content in it. The >> construct appends information to a file.

To select a temporary directory

```text
$ echo "%_tmppath $HOME/tmp" >> $HOME/.rpmmacros
```

To set any compiler optimization flags (here, we are using an Athlon processor as an example), we will use

```text
$ echo "-o3 -march=athlon" >> $HOME/.rpmmacros
```

To rebuild a src.rpm file as a regular user, you would use

```text
$ rpmbuild --recompile packagename.src.rpm
```

After a successful build, you will find the binary file(s) in ~/redhat/RPMS/athlon. You can install them as root with

```text
# rpm -Uvh --replacepkgs --replacefiles packagename.rpm
```

If the build fails, the error message will point you to a solution (usually a dependency has not been satisfied). You will find that a lot of the packages named with -devel will be needed before you compile from source code. Install the package for the missing dependency and retry the compile.

## Working with Source RPM Files

You might want to modify a source package for your own uses such as adding documentation, changing default settings, or patching the source code itself. Fedora Core provides the source code to its distribution in the form of source RPM files. You can access the source code on disks 4 and 5 of the downloadable CD images or obtain them from the Fedora Core FTP site.

> **TIP**
> 
> An important part of the RPM file is called the .spec file, a specification file. It tells RPM how to behave with the particular source files during compilation, installation, and erasure.

As an example, we'll use information that was found at http://elektron.its.tudelft.nl/~rbos36/mdkfree type2.html (the page has now been removed by the author) to modify the freetype2 library provided with Fedora Core in order to enable the bytecode interpreter. The code for the interpreter has been disabled by default because of redistribution licensing concerns that don't affect individual use. Enabling the interpreter will result in improved rendering of the TrueType fonts. We used the file from Red Hat 7.3 as our example, but the source file from FC4 should work as well.

Begin work by first installing the source RPM package with `rpm -i`. (Note that here we are building as root to follow the example from the web page; you should typically build packages as a regular user.) In our example, obtain the `freetype-2.1.9-2.src.rpm` and install it with `rpm -i`. The source code files are placed in `/usr/src/redhat/SOURCES`.

Copy the source file (it's a compressed tar file) to `/tmp`, and then `cd` (change directories) there to unpack and modify it:

```text
# cp freetype-2.1.9.tar.bz2 /tmp
# cd /tmp
```

Because it's a .bz2 (BZip2 compressed) tar file, un-tar it with

```text
# tar xjvf freetype-2.1.9.tar.bz2
```

and `cd` to the new directory:

```text
# cd freetype-2.1.9
```

Using the text editor of your choice, edit the file `include/freetype/config/ftoption.h` and find the line

```text
#undef  TT_CONFIG_OPTION_BYTECODE_INTERPRETER
```

Change it to

```text
#define  TT_CONFIG_OPTION_BYTECODE_INTERPRETER
```

Save it and exit the text editor.

Next, re-create the compressed archive:

```text
# cd /tmp
# tar cfj freetype-2.1.9.tar.bz2 ./freetype-2.1.9/
```

Put it back in your source directory:

```text
# mv freetype-2.1.9.tar.bz2 /usr/src/SOURCES
```

Now edit the `.spec` file in `/usr/src/redhat/SPECS` to change the line beginning with `Release` to increment the number found there. (We are changing the version number by doing this, so it will not conflict with the version of the application we will be replacing.) Make any changes to the `%description` line to describe your changes if you desire, and save the file.

Build the binary RPM with

```text
# rpmbuild -bb freetype.spec
```

During the build process, RPM will detect a patch and ask you about the patch; press `y` for "yes" to continue.
