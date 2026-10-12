# CAUTION

> Additional related files rely on Qt-development files in order to run. Though the RPM version does install the necessary headers for Qt, these may not be located in the same place as would the compiled version of Qt. If you are installing Qt from source, the install program might place them elsewhere. This is sometimes the case with the Red Hat version of the Qt libraries. Programs that rely on the Qt headers may look for them in one location and not find them.

# ## Compiling KDE Source Code

For enthusiasts or purists who still insist on compiling code, KDE provides the full KDE source for inspection and modification. As with the installation of most any source code, there are just a few steps to follow to compile and install the newly created binaries.

The files you will want to download will have either a .tar.gz or a .tar.bz2 extension. These extensions identify the files as being tarred and zipped for archival purposes. There may also be files with different extensions, and these tar files can be uncompressed in the same manner.

Files archived as tar source files normally install into /usr/local/kde by default. You can override this setting by using the --prefix option of the configure script. If you prefer setting the default directory to /opt/kde, you may do so when configuring. The following are some simple steps to follow when installing the source code of KDE. You must repeat each of these steps for every tarred and zipped package:

+   1. Unpack the packages by entering `tar -xvzf <packagename>.tar.gz`. If the packages end with a different extension, use the appropriate command. You may also unpack the packages by entering `bunzip2 -c <packagename>.tar.bz2 | tar xvf -`. Both methods work equally well. The choice is a matter of preference.

+   2. Change directories to the newly created package directory by entering `cd <packagename>`.

+   3. Configure the package by entering `./configure`. This command is where you add any extra flags or options. To define a new default directory, enter `./configure --prefix=/opt/kde`.