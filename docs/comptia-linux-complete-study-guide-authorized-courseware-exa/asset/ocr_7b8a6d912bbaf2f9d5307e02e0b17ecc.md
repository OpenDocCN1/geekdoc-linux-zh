To set the `LD_LIBRARY_PATH` environment variable using the bash shell, you can type a command like this:

```
$ export LD_LIBRARY_PATH=/usr/local/testlib:/opt/newlib
```

This line adds two directories, /usr/local/testlib and /opt/newlib, to the search path. You can specify as few or as many directories as you like, separated by colons. These directories are added to the start of the search path, which means they take precedence over other directories. This fact is handy when you're testing replacement libraries, but it can cause problems if users manage to set this environment variable inappropriately.

You can set this environment variable permanently in a user's shell startup script files, as described in Chapter 9. Doing so means the user will always use the specified library paths in addition to the normal system paths. In principle, you could set the `LD_LIBRARY_PATH` globally; however, using `/etc/ld.so.conf` is the preferred method of effecting global changes to the library path.

Unlike other library path changes, this one doesn't require that you run `ldconfig` for it to take effect.

# ## Correcting Problems

Library path problems usually manifest as a program's inability to locate a library. If you launch the program from a shell, you'll see an error message like this:

```
$ gimp

gimp: error while loading shared libraries: libXinerama.so.1: cannot
open shared object file: No such file or directory
```

This message indicates that the system couldn't find the `libXinerama.so.1` library file. The usual cause of such problems is that the library isn't installed, so you should look for it using commands such as `find` (described in Chapter 4, “Managing Files”). If the file isn't installed, try to track down the package to which it should belong (a Web search can work wonders in this task) and install it.

If, on the other hand, the library file is available, you may need to add its directory globally or to `LD_LIBRARY_PATH`. Sometimes the library's path is hard-coded in the program's binary file. (You can discover this using `ldd`, as described shortly in “Library Management Commands.”) When this happens, you may need to create a symbolic link from the location of the library on your system to the location the program expects. A similar problem can occur when the program expects a library to have one name but the library has another name on your system. For instance, the program may link to `biglib.so.5`, but your system has `biglib.so.5.2` installed. Minor version-number changes like this are usually inconsequential, so creating a symbolic link will correct the problem:

```
# ln -s biglib.so.5.2 biglib.so.5
```

You must type this command as `root` in the directory in which the library resides. You must then run `ldconfig`, as described in the next section.