Now complete Exercise 19.1, which gives you experience in using the ldd command.

# EXERCISE 19.1

# Viewing Library References

Here's a simple puzzle that will give you an opportunity to use the ldd command. Use the ldd command to view library references associated with arbitrary executables in the /bin directory and /usr/bin directory. Can you see a pattern that distinguishes the source of the executables?

# Specifying Library Paths

If the loader is unable to locate a library required by a program, it prints an error and handles the loading process. If the library resides on the system, you can inform the loader of its location by setting the environment variable LD_LIBRARY_PATH. For example, to specify that the loader should search the directories /usr/local/lib and /usr/local/otherlib for required libraries, issue the command

```
export LD_LIBRARY_PATH=/usr/local/lib:/usr/local/otherlib
```

The specified directory or directories are searched in the default directories, which needfore not be explicitly specified.

# Installing Shared Libraries

When you install an RPM package that includes a shared library, the installation script should automatically update the shared library configuration. However, if you install a non-RPM package you may need to revise the shared library configuration manually.

The shared library configuration resides in the file /etc/ld.so.conf, which contains a list of directories that contain shared libraries, each directory on each line. Here are the contents of a typical ld.so.conf file:

+   * /usr/lib
* /usr/i486-linux-libc5/lib
* /usr/X11R/lib
* /usr/i486-linuxout/lib

www.sybex.com