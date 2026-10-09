# # uClibc

As with glibc, uClibc contains a number of libraries. Look in your `$${PREFIX}/uclibc/lib` directory for the entire list. It contains the same four different types of files as the glibc directory.

Because uClibc is meant to be a glibc replacement, the names and uses of the uClibc components are identical to the glibc components. Hence, you can use Table 6-2 (shown previously) to research uClibc components. Note, however, that not all glibc components are implemented by uClibc. uClibc implements only *ld, libc, libcrypt, libdl, libm, libpthread, libresolv, and libutil*. Use the same method as described for glibc to identify the uClibc components you will need on your target.

Having determined the list of components you need, you can now copy them and their relevant symbolic links to the *lib* directory of your target's root filesystem. The following set of commands copies the essential uClibc components:

```
```
$ cd $${PREFIX}/uclibc/lib
$ for file in libc libc libc-nonshared libdl libcres libm libpthread libresolv
>        do
>         cp $file*.so $${PREFIX}/rootfs/lib
>         cp -d $file.so.$${*} $${PREFIX}/rootfs/lib
> done
```
```

The commands are likely to report that two files haven't been found:

```
```
cp: libcNonshared.so.[*-*]: No such file or directory
cp: libc*.so: No such file or directory
```
```

This is not a problem, because these files are not supposed to exist. The set of commands just shown is meant to be easy to type in, but you could add conditional statements around the *cp* commands if you prefer not to see any errors.

As with glibc, you can modify the list of libraries you copy according to your requirements. Note that, in contrast to glibc, you will not save much space by copying only a select few uClibc components. For the control module previously mentioned, for instance, the root filesystem's *lib* directory weighs only around 300 KB when *all* the uClibc components are copied. The following commands copy all uClibc's components to your target's root filesystem:

```
```
$ cd $${PREFIX}/uclibc/lib
$ cp *.so $${PREFIX}/rootfs/lib
$ cp -d *.so.[*-*] $${PREFIX}/rootfs/lib
```
```

There is no need to strip uClibc components, since they were already stripped by uClibc's own build scripts. You can verify this using the *file* command.