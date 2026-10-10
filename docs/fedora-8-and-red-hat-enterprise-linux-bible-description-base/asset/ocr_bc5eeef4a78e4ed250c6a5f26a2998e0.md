# Installing software in tar.gz or tar.bz2 formats

Here are some generic instructions that you can use to install many Linux software packages that are in the *gzip* or *tar* format:

+   Get the source code package from the Internet or from a CD distribution and copy it into an empty directory (preferably using a name that identifies the package).

+   To check the contents of your *tar* archive before extracting it to your hard drive, you could use the following command:

```
```bash
# tar tvf package.tar.gz
```
```

+   Assuming the file is compressed using *gzip*, uncompress the file using the following command:

```
```bash
# gunzip package.tar.gz
```
```

The result is that the package is uncompressed and the *.gz* is removed from the package name (for example, *package.tar*). (If your package ends in *bz2*, use the *bzip2* command instead of *gunzip* shown above.)

+   From the resulting *tar* archive, run the *tar* command as follows:

```
```bash
# tar xvf package.tar
```
```

This command extracts the files from the archive and copies them to a subdirectory of the current directory. (Using *tar xvfz package.tar.gz* you can do steps 2 and 3 in one step. For a compressed *bzip2* file, run *tar xvfj package.tar.bz2* instead.)

+   Change directories to the new subdirectory created in Step 3, as follows:

```
```bash
# cd package
```
```

+   Look for a file called *INSTALL* or *README*. One of these files should give you instructions on how to proceed with the installation. In general, the *make* command is used to install the package. Here are a few things to look for in the current directory:

If there is a *Makefile*, try running:

```
```bash
# ./configure --prefix=/usr/local
# make all
```
```

If there is an *Imakefile*, try running:

```
```bash
# xmkmf -a
# make all
```
```

If there is a *Makefile*, try running:

```
```bash
# make all
```
```