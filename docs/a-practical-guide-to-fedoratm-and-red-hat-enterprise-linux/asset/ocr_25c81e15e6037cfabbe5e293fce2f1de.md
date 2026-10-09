want to wait a while before removing the old kernel to make sure that no problems arise with the new one.

+   3. When you are satisfied with the new kernel, remove the old kernel using **rpm** with the `-e` option; you must specify the kernel version number. If necessary, you can manually remove an old kernel by removing files whose names contain the release number from `/boot` or `/` (root). Remove information about the old kernel from **grub.conf** (page 590). Removing the kernel manually is not recommended because it is too easy to miss a file and because it does not remove the kernel from the RPM database.

# Installing Non-rpm Software

Most software that is not in RPM format comes with detailed instructions on how to configure, build (if necessary), and install it. Some binary distributions (those containing prebuilt executables) that run on Fedora/RHEL require you to unpack the software from the root directory (i.e., you must `cd /` before unpacking it).

# The /opt and /usr/local Directories

Some newer application packages include scripts that install themselves automatically into a directory hierarchy under `/opt`, with files in a `/opt` subdirectory that is named after the package and executables in `/opt/bin` or `/opt/package/bin`.

Other software packages allow you to choose where you unpack them. Because many different people develop software for Linux, there is no consistent method for installing it. As you acquire software, install it on the local system in as consistent and predictable a manner as possible. The standard Linux file structure has a directory hierarchy under `/usr/local` for binaries (`/usr/local/bin`), manual pages (`/usr/local/man`), and so forth. Because many GNU build tools search the `/usr/local` hierarchy by default and could find the wrong version of a utility if you install developer tools there, putting these tools in `/opt` is a good idea.

To prevent confusion later and to avoid overwriting or losing the software when you install standard software upgrades, avoid installing nonstandard software in standard system directories (such as `/usr/bin`). On a multiserver system, make sure users know where to find the local software and advise them whenever you install, change, or remove local tools.

# GNU Configure and Build System

The GNU Configure and Build System makes it easy to build a program that is distributed as source code (see `www.gnu.org/software/autoconf/`). This process requires a shell, **make** (`make` package), and **gcc** (the GNU C compiler; `gcc` package). You do not need to work with `root` privileges except to install the program.