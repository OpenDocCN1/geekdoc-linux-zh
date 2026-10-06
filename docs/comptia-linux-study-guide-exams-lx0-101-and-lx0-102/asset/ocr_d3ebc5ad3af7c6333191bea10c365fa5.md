+   12. What is the preferred method of adding a directory to the path library for users?

+   A. Modify the LD_LIBRARY_PATH environment variable in a global shell script.

+   B. Add the directory to the /etc/ld.so.conf file, and then ldconfig to add.

+   D. Create a symbolic link from directory to one that's already on the library path.

+   E. Type ldd /new/dir, where /new/dir is the directory you want to add.

+   13. You prefer the look of GTK+ widgets to Qt widgets, would you want to substitute the GTK+ libraries for the Qt libraries on your system. How would you do?

+   A. You must type ldconfig --makesub=qt,gtk. This command substitutes the GTK+ libraries for the Qt libraries at load.

+   B. You must uninstall the Qt libraries and re-install the GTK+ packages with the --substitute qt option to rpm or the --replace qt option to dpkg.

+   C. You must note the filenames of the Qt libraries, uninstall the packages, and create symbolic links from the Qt libraries to the GTK+ libraries.

+   D. You can't easily do these; libraries can't be arbitrarily exchanged for one another. You would need to rewrite all the Qt-using programs to use GTK+.

+   E. You must reboot the computer and pass the subst=qt,gtk option to the kernel. This causes the kernel to make the appropriate substitutions.

+   14. A user types kill -9 11287 at a bash prompt. What is the probable intent, assuming the user typed the correct command?

+   A. To cut off a network connection using TCP port 11287

+   B. To display the number of processes that have been killed with signal 11287 in the last nine days

+   C. To cause a server with process 11287 to reload its configuration file

+   D. To terminate a misbehaving or hung program with process ID 11287

+   E. To increase the priority of the program running with process ID 11287

+   15. What programs might you use to learn what your system's load average is? (Select two.)

+   A. ldd

+   B. load

+   C. top

+   D. uptime

+   E. 1a