+   * The **dmalloc** library and utility must be installed on your embedded target.

+   * Certain environment variables that the **dmalloc** library references must be defined before running your application on the target.

Although it is not strictly necessary, you should include **dmalloc.h** in your application program. This allows **dmalloc** to include file and line number information in the output.

Link your application against the **dmalloc** library of your choice. The **dmalloc** package can be configured to generate several different libraries, depending on your selections during package configuration. In the examples to follow, we have chosen to use the **libd malloc.so** shared library object. Place the library (or a symlink to it) in a path where your compiler can find it. The command to compile your application might look something like this:

```
```
$ ppc-82mx-gcc -g -Wall -o mtest_ex -L../d malloc-5.4.2/ \
    -ld malloc mtest_ex.c
```
```

This command line assumes that you've placed the **d malloc** library (**libd malloc.so**) in a location searched by the `-L` switch on the command line—namely, the `../d malloc-5.4.2` directly just above the current directory.

To install the **d malloc** library on your target, place it in your favorite location (perhaps `/usr/local/lib`). You might need to configure your system to find this library. On our example PowerPC system, we added the path `/usr/local/lib` to the `/etc/ld.so.conf` file and invoked the **ldconfig** utility to update the library search cache.

The last step in preparation is to set an environment variable that the **d malloc** library uses to determine the level of debugging that will be enabled. The environment variable contains a debug bit mask that concatenates a number of features into a single convenient variable. Yours might look something like this:

```
`DMALLOC_OPTIONS=debug=0x4f4ed03,inter=100,log=d malloc.log`
```

Here, `debug` is the debug-level bit mask, and `inter` sets an interval count at which the **d malloc** library performs extensive checks on itself and the heap. The **d malloc** library writes its log output to the file indicated by the `log` variable.

The **d malloc** package comes with a utility to generate the **DMALLOC_OPTIONS** environment variable based on flags passed to it. The previous example was