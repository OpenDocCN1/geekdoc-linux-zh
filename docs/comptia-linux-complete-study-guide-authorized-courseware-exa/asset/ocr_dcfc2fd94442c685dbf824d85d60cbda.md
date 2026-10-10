# ## Library Management Commands

Linux provides a pair of commands that you're likely to use for library management. The `ldd` program displays a program's shared library dependencies—that is, the shared libraries that a program uses. The `ldconfig` program updates caches and links used by the system for locating libraries—that is, it reads `/etc/ld.so.conf` and implements any changes in that file or in the directories to which it refers. Both of these tools are invaluable in managing libraries.

# ### Displaying Shared Library Dependencies

If you run into programs that won't launch because of missing libraries, the first step is to check which libraries the program file uses. You can do this with the `ldd` command:

```
```
$ ldd /bin/ls
libt.so.1 => /lib/libt.so.1 (0x0000002a9566c000)
libncurses.so.5 => /lib/libncurses.so.5 (0x0000002a95784000)
libacl.so.1 => /lib/libacl.so.1 (0x0000002a958ea000)
libc.so.6 => /lib/libc.so.6 (0x0000002a959f1000)
libpthread.so.0 => /lib/libpthread.so.0 (0x0000002a95c17000)
/lib64/ld-linux-x86-64.so.2 (0x0000002a95556000)
libattr.so.1 => /lib/libattr.so.1 (0x0000002a95da0000)
```
```

Each line of output begins with a library name, such as `libt.so.1` or `libncurses.so.5`. If the library name doesn't contain a complete path, `ldd` attempts to find the true library and displays the complete path following the `=>` symbol, as in `/lib/libt.so.1` or `/lib/libncurses.so.5`. You needn't be concerned about the long hexadecimal number following the complete path to the library file. The preceding example shows one library (`/lib64/ld-linux-x86-64.so.2`) that's referred to with a complete path in the executable file. It lacks the initial directory-less library name and `=>` symbol.

The `ldd` command accepts a few options. The most notable of these is probably `-v`, which displays a long list of version information following the main entry. This information may be helpful in tracking down which version of a library a program is using, in case you have multiple versions installed.

Keep in mind that libraries can themselves depend on other libraries. Thus, you can use `ldd` to discover what libraries are used by a library. Because of this potential for a dependency chain, it's possible that a program will fail to run even though all its libraries are present. When using `ldd` to track down problems, be sure to check the needs of all the libraries of the program, and all the libraries used by the first tier of libraries, and so on, until you've exhausted the chain.

The `ldd` utility can be run by ordinary users, as well as by `root`. You must run it as `root` if you can't read the program file as an ordinary user.