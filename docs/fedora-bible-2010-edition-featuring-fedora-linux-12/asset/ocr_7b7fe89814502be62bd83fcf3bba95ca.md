The `--rebuild` option to `rpmbuild` can be used to rebuild the RPM without installing it first. The resulting binary will be in `rpmbuild/RPMS/arch`, where `arch` is replaced by i386 or other architecture for which you are building the RPM.

# Installing software in tar.gz or tar.bz2 formats

Here are some generic instructions that you can use to install many Linux software packages that are in the `gzip` or tar format:

+   1. Get the source code package from the Internet or from a CD distribution and copy it into an empty directory (preferably using a name that identifies the package).

+   2. To check the contents of your tar archive before extracting it to your hard drive, you could use the following command:

```
# tar ztvf package.tar.gz
```

> **NOTE:** Use the command `tar tvjf` if the file is compressed using `bzip2`.

+   3. Assuming the file is compressed using `gzip`, uncompress the file using the following command:

```
# gunzip package.tar.gz
```

The result is that the package is uncompressed and the `.gz` is removed from the package name (for example, `package.tar`). (If your package ends in `bz2`, use the `bzip2` command instead of `gunzip`.)

+   4. From the resulting `tar` archive, run the `tar` command as follows:

```
# tar xvf package.tar
```

This command extracts the files from the archive and copies them to a subdirectory of the current directory. (Using `tar xvfz package.tar.gz` you can do Steps 2 and 3 in one step. For a compressed `bzip2` file, run `tar xvjf package.tar.bz2` instead.)

+   5. Change directories to the new subdirectory created in Step 3, as follows:

```
# cd package
```

+   6. Look for a file called `INSTALL` or `README`. One of these files should give you instructions on how to proceed with the installation. In general, the `make` command is used to install the package. Here are a few things to look for in the current directory: If there is a `Make.in` file, try running:

```
# ./configure --prefix=/usr/local
# make all
```

If there is a `Imake` file, try running: