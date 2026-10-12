you'll also learn the programming language used to write the package. If you see `.c` and `.h` files, that means the source files are in the C programming language used to write many open-source software packages.

To extract the contents of the compressed `tar` archive, type the following `tar` command:

```
tar zxvf xmms*.gz
```

You'll again see the long list of files as they are extracted from the archive and copied to the appropriate directories on your hard drive.

Now you're ready to build the software.

# Building the software from source files

After you unpack the compressed `tar` archive, all source files will be in a directory whose name is usually that of the software package with a version-number suffix. For example, the XMMS version 1.2.7 source files are extracted to the `xmms-1.2.7` directory. To start building the software, change directories with the following command:

```
cd xmms*
```

You don't have to type the entire name — the shell can expand the directory name and change to the `xmms-1.2.7` directory.

Nearly all software packages come with some sort of `README` or `INSTALL` file — a text file that tells you how to build and install the package. XMMS is no exception; it comes with a `README` file you can peruse by typing `more README`. There is also an `INSTALL` file that contains instructions for building and installing XMMS.

![](bbox=[0.12, 0.75, 0.22, 0.9])

Most open-source software packages, including XMMS, also come with a file named `COPYING`. This file contains the full text of the GNU General Public License (GPL), which spells out the conditions under which you can use and redistribute the software. If you're not familiar with the GNU GPL, read this file and show the license to your legal counsel for a full interpretation and an assessment of applicability to your business.

To build the software package, follow the instructions in the `README` or `INSTALL` file. For the XMMS package, the `README` file lists some of the prerequisites (such as libraries) and tells you what commands to type to build and install the package. In the case of XMMS, the instructions tell you to use the following steps: