+   TAR files work on all Linux and Unix flavors, while not all Linux machines (such as Debian machines) can deal with RPM files by default.

Disadvantages of TAR format:

+   Difficult to keep track of files installed by a TAR file package

+   Difficult to check for file corruption or modification

# Try It Out Installing a Binary Package in TAR Format

In order to help us understand how to deal with TAR packages we'll demonstrate the installation of a small file package that tells us what kind of web server a web site is running on.

+   Firstly we downloaded the file chkwew-0.4.3.tar.gz from www.sourceforge.net, and placed it in our /usr/local directory (though we could have put it anywhere).

+   Next we to the /usr/local directory and uncompress the TAR file (you can tell it's been compressed using GZIP, as it has a .gz suffix. (This step isn't always necessary).

```
# gzip -dv pychkwew_0.4.TAR.gz
pychkwew_0.4.TAR.gz: 81.6% -- replaced with pychkwew_0.4.TAR
```

The -dv options mean:

+   -d This decompresses the file.

+   -v This uses verbose mode, so it prints its progress to the screen.

+   -f This option forces the overwriting of old (existing) files with their newer counterparts.

This creates an uncompressed TAR file called chkwew-0.4.3.tar

+   Now we 'unTAR' the package to release the files with it. This is done with the following command. You'll see a list of the files released:

```
# TAR -xvxf pychkwew_0.4.TAR
pychkwew/
pychkwew/CVS/
......
pychkwew/README
pychkwew/TODO
pychkwew/VERSION
```