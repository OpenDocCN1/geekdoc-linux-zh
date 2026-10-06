# Using RPM

Alternatively, you can use a pipe to link these two commands together without creating an intermediary file:

```
$ rpm2cpio samba-3.6.5-86.fc17.1.src.rpm | cpio -i --make-directories
```

In either case, the result is an extraction of the files in the archive in the current directory. In the case of binary packages, this is likely to be a series of subdirectories that mimic the layout of the Linux root directory—that is, usr, libc, etc., and so on, and precisely which directories are included in the package. For a source package, the result of the extraction process is likely to be a source code tarball, a .spec file (which holds information) RPM uses to build the package), and perhaps few some patches.

![](bbox=[0.166, 0.303, 0.225, 0.335])

When you're extracting data from an RPM file using rpm2cpio and cpio, create a holding subdirectory and extract the data into this subdirectory. This practice will ensure that you can find all the files. If you extract your files in your home directory, some might get lost your other files. If you extract files as root in the (/) directory, you could conceivably overwrite files that you want to keep.

Another option for extracting data from RPMs is to use alien, which is described later in “Converting Package Formats.” This program can convert an RPM into a Debian package or a tarball.

# Using Yum

Yum (http://yum.baseurl.org), mentioned earlier, is one of several meta-packagers—it enables you to install a package and all its dependencies using a single command. When using Yum, you don't even need to search in or download the package files, because Yum does this for you in one or more repositories—Internet sites that hold RPM files for a particular distribution.

Yum originated from the obscure Yellow Dog Linux distribution, but it's been adopted by Red Hat, CentOS, Fedora, and some other RPM-based distributions. Yum is not used by RPM-based distributions; though SUSE and Mandriva have just two, each their own meta-apts. Debian-based distributions generally employ the Advanced Package Tools (APT), as described later in “Using apt-get.” Nonetheless, because of the popularity of Red Hat, CentOS, and Fedora, knowing Yum can be valuable.

The best way to use Yum is with the yum command, which has the following syntax:

```
yum [options] [command] [package...]
```

Which options are available depend on the command you use. Table 2.3 describes common yum commands.