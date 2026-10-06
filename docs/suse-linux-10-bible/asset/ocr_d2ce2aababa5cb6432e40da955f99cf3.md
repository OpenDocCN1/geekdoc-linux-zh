# Chapter 2 ♦ Linux Fundamentals 73

problems, because these two versions are binary compatible. But in many cases although you may not be able to install the binary RPM, you may be able to take a source package and rebuild it according to needs. In the simplest case, you would do this (as root):

```
rpmbuild --clean --rebuild packagename.src.rpm
```

You will find that in the directory /usr/src/packages/RPMS, in the subdirectories corresponding to your architecture (i386 if you are on x86), there is a brand-new RPM package that you can install. Again, you will need to have the development tools installed for this work.

Working with packages is covered in detail in Chapter 12.

![](bbox=[0.122, 0.325, 0.193, 0.368])

# Compiling Source Packages

You will often find materials distributed as zipped tar archives. These are files that will usually have names as filename.gz or filename.tar.gz. To extract all the files from this archive, copy it to an empty directory somewhere and use the tar command to unpack it, something like the following example:

```
mkdir unpack
cp filename.tgz unpack/
cd unpack
tar zvzf filename.tgz
```

Usually, you will then find that a new directory has been created with all the contents of the package inside—if you are lucky, there will be a document giving details about how to build the package. Very often (but not always) the way to proceed is to do the following commands:

```
./configure
make
make install
```

You will need to have the development tools installed for this work.

# Connecting over the Network

Traditionally the way to connect to a remote machine and work on it was Telnet. Telnet is inherently insecure because it sends passwords in plain text across the network; SUSE systems do not have a Telnet server enabled by default. If you want to log in remotely, you should use ssh (secure shell).