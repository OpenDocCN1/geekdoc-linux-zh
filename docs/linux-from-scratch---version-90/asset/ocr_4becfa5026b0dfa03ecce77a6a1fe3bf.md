# 6.3.2. Install in Separate Directories

This is a simplistic management framework that does not need any extra package to manage the installations. Each package is installed in a separate directory. For example, package-libfoo-1 is installed in /usr/pkg/foofoo-1 and a symlink is made from /usr/pkg/libfoo to /usr/pkg/libfoo-1. When installing a new version of libfoo-1.2, it is installed in /usr/pkg/libfoo-1.2 and the previous symlink is replaced by a symlink to the new version.

Environment variables such as PATH, LD_LIBRARY_PATH, MANPATH, INFOPATH and CPPFLAGS need to be expanded using /usr/pkg/foo. For more than a few packages, this scheme becomes unmanageable.

# 6.3.3. Symlink Style Package Management

This is a variation of the previous package management technique. Each package is installed alongside the previous scheme. Instead of making the symlink, each file is symlinked into the /usr hierarchy. This removes the need to expand the environment variables. Though the symlinks can be created by the user to automate the creation, many package managers have been using this approach. A few of the popular ones include Stow, Epkg, Graft, and Depot.

The installation needs to be fake, so that the package that it is installed in /usr in reality it is installed in the /usr/pkg hierarchy. Installing in this manner is not a trivial task. For example, consider that you are installing a package libfoo-1.1. The following instructions may not install the package properly:

```
./configure --prefix=/usr/pkg/libfoo/1.1
make
make install
```

The installation will work, but the dependent packages may not link to libfoo as you expect. If you compile a package that you may notice it is linked to /usr/pkg/libfoo-1.1/lib/libfoo.so.1 instead of /usr/lib/libfoo.so.1 as you would expect. The correct approach is to use the DESTDIR strategy to fake installation of the package. This approach works as follows:

```
./configure --prefix=/usr
make
DESTDIR=/usr/pkg/libfoo/1.1 make
```

Most packages support this approach, but there are some who do not. For the non-compliant packages, you may either need to manually install the package, or you may find that it is easier to install some problematic packages into /opt.

# 6.3.4. Timestamp Based

In this technique, a file is timestamped before the installation of the package. After the installation, a simple use of the find with the appropriate options can generate a log of all the files installed after the timestamp file was created. A package manager with this approach is install-log.

Though this scheme has the advantage of being simple, it has two drawbacks. If, during installation, the files are installed with any timestamp other than the current time, files will not be tracked by the package manager. Also, this scheme can only be used when one package is installed at a time. The logs are not reliable if two packages are being installed on two different consoles.

# 6.3.5. Tracing Installation Scripts

In this approach, the commands that the installation scripts perform are recorded. There are two techniques that one can use: