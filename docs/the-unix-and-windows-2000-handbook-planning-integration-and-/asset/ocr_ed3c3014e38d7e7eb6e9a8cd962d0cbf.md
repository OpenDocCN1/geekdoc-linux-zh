Interface (APACI) greatly simplifies the compilation and installation process. The APACI generates the correct configuration files for the operating system. The following Solaris installation procedures would be the same for any AIX, HPUX, or Red Hat Linux workstation.

# Downloading the Packages

There are two requirements for installing a source distribution of the Apache Web Server. The first requirement is a directory that has approximately 30MB of free disk space to download, unpack, and compile the sources. The second requirement is an ANSI-C compiler. Enter the following command to determine if your Solaris system contains an ANSI-C compiler:

```
```text
%pkginfo SPROcc
application SPROcc      SPARCompiler C 3.0.1
```
```

The above indicates that the SunSoft ANSI-C compiler is installed. If you do not have the SunSoft compiler installed (ERROR: information for SPROcc was not found), www.gnu.org contains links to binary distributions of the GNU C compiler for Solaris, AIX, and HPUX. This package can be downloaded, uncompressed, and added to your Solaris system with the pkgadd command. The GNU C compiler package will be installed under the /usr/local directory.

Now that we have all the required pieces, we need to download the Apache Web Server sources. The latest stable version of the Apache Web Server can be downloaded from http://www.apache.org. The distribution we downloaded is apache_1.3.9.tar.gz. The gz suffix indicates that this file is compressed. To uncompress it, execute the following command:

```
```text
#gunzip apache_1.3.9.tar.gz
```
```

We are left with the file apache_1.3.9.tar. Now we must process this file with the following command:

```
```text
#tar -xvf apache_1.3.9.tar
```
```

The result of this command is a new directory called apache_1.3.9. We are now ready to configure, compile, and install the Apache Web Server.

# Apache Web Server Installation

First, change directory (cd) into the top-level directory (apache_1.3.9) of the Apache server distribution. Configuration of the server, compilation and installation will require only three commands using APACI. We are building a server that will include support for DSOs and add a few modules that are not included in the default server.