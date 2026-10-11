```
if ((debugging & DEBUG_FILE) != 0) . . . In the I/O part of the program
if ((debugging & DEBUG_MEM) != 0) . . . In the memory manager
```

It is up to you whether to use a single variable with flag bits, separate variables, or even a debugging array, indexed by symbolic constants (preferably from an enum).

The cost of leaving the debugging code in your production executable is that the program will be larger. Depending on the placement of your debugging code, it may also be slower since the tests are always performed, but are always false until debugging is turned on. And, as mentioned, it may be possible for someone to learn about your program, which you may not want. Or worse, a malevolent user could enable so much debugging that the program slows to an unusable stare! (This is called a denial of service attack.)

The benefit, which can be great, is that your already installed program can be re-invoked with debugging turned on, without requiring you to build, and then download, a special version to your customer site. When the software is installed in remote places that may not have people around and all you can do is access the system remotely through the Internet (or worse, a slow telephone dial-in!), such a feature can be a lifesaver.

Finally, you may wish to mix and match: use conditionally compiled debugging code for fine-grained, high-detail debugging, and save the always-present code for a coarser level of output.

# 15.4.2.2 Use Special Environment Variables

Another useful trick is to have your application pay attention to special environment variables (documented or otherwise). This can be particularly useful for testing. Here’s another example from our experience with gawk, but first, some background.

gawk uses a function named optimal_bu fsize() to obtain the optimal buffer size for I/O. For small files, the function returns the file size. Otherwise, if the filesystem defines a size to use for I/O, it returns that (the st_blksize member in the struct stat, see Section 5.4.2, “Retrieving File Information,” page 141). If that member isn’t available, optimal_bu fsize() returns the B U F S I Z E constant from <stdio.h>. The original function (in posix/gawkmisc.c) looked like this: