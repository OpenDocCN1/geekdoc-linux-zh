```
{
    if(d->name)
    {
        printf("Destroying: %s\n", d->name);
        free(d->name);
    }
    free(d);
}
```

The object offers three interface functions:

+   ♦ init to allocate any necessary storage and initialize the object
+   ♦ show to display the object (here, it simply prints a message)
+   ♦ destroy to free any storage

To build the shared library named libdobj.so, follow these steps:

+   1. Compile all source files with the -fPIC flag. In this case, compile the dynobj.c file by using this command:
+      ```
+      gcc -fPIC -c dynobj.c
+      ```
+   2. Link the objects into a shared library with the -shared flag, and provide appropriate flags for the linker. To create the shared library named libdobj.so.1, use the following:
+      ```
+      gcc -shared -Wl,-soname,libdobj.so.1 -o libdobj.so.1.0
+      dynobj.o
+      ```
+   3. Set up a sequence of symbolic links so that programs that use the shared library can refer to it with a standard name.
+      For the sample library, the standard name is libdobj.so, and the symbolic links are set up by using these commands:
+      ```
+      ln -sf libdobj.so.1.0 libdobj.so.1
+      ln -sf libdobj.so.1 libdobj.so
+      ```
+   4. When you test the shared library, define and export the LD_LIBRARY_PATH environment variable by using the following command:
+      ```
+      export LD_LIBRARY_PATH=`pwd`:$LD_LIBRARY_PATH
+      ```

After you test the shared library and are satisfied that the library works, copy it to a standard location, such as /usr/local/lib, and run the ldconfig utility to update the link between libdobj.so.1 and libdobj.so.1.0.