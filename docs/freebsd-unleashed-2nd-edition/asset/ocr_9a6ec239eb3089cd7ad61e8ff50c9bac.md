TABLE 14.3  Continued

| Target | Action |
| :--- | :--- |
| configure | Runs the configure script, which prepares the source for building |
| build | Compiles the source |
| install | Copies the compiled program and related files to their destinations |
| deinstall | Deletes all files as listed in the packing list |
| clean | Deletes the work subdirectory |

Typing make extract, for example, will download the source file, match its MD5 checksum, and unpack it. Although there are other targets (listed in /usr/ports/Mk/bsd.port.mk), you won’t need to use any of them under most circumstances.

After each step in the process is complete (except for fetch and checksum), a file is created in the work subdirectory of the form .extract_done. This is how the system keeps track of which steps are completed. To see whether the fetch step is done, it simply checks for the existence of the file in /usr/ports/distfiles. The extract step runs the checksum step implicitly. After that, the steps are sequential and independent, and they check for prerequisite steps by looking for the appropriate .*_done files.

If you need to make any changes to the source before compiling, you can run make patch, thus bringing the source up to where it’s ready to compile, and then make whatever changes you like. Then, you can complete the process with make.

Dependencies are handled automatically by the ports, just as with the packages. Any dependencies are read from the makefile during the fetch phase and then downloaded, built, and installed. You will get feedback in the build output each time it encounters a dependency, regardless of whether that dependency is installed already.

After a port is installed, an entry is made in the /var/db/pkg database; for all intents and purposes, it is now a package. You can use the pkg_* tools on it to gather information and compare its version, just as with packages installed from within sysinstall.

There is a deinstall target in the ports (make deinstall). This target is used when the installed port version is the same as the one in the makefile—in essence, you’re deinstalling exactly the same software package you installed. If you update your ports so that the version of a port (in the makefile) is higher than the installed version, you can’t use make deinstall to delete it. Instead you have to use pkg_delete, the same way as you would a package.

# ## Upgrading a Port

If the version of a port has changed, you can simply use make install to install it over the old version. This can be a bad idea, however, because most of the installed files will be the same from one version to another, so if you try to delete (using pkg_delete) an older version of the same port or package while a newer one is installed over it, you will end up deleting most of the newer version as well. If you have pkg_version output like the