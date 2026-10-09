If you hang around the FreeBSD community for a while, you'll hear all sorts of stories about special methods people use for building FreeBSD. You'll hear anecdotal evidence that one method is faster, more efficient, or somehow mystically “better” than the standard. While you are certainly free to use any build method that strikes your fancy, the only method supported by the FreeBSD Project is that documented at the end of `/usr/src/UPDATING`. If you follow some other procedure and have trouble, you'll be referred to the documented procedure.

# **Build the World**

First, build the new userland:

```
# cd /usr/src
# make buildworld
```

The `make buildworld` command builds from source the basic tools needed to build the system compiler and then builds the compiler and associated libraries. Finally, it uses the new tools, compiler, and libraries to build all the software included in a core FreeBSD install. (This is much like building a car starting with the instruction, “Dig iron ore out of the ground.”) The buildworld places its output under `/usr/obj`. It can take anywhere from one to several hours, depending on your hardware. You can continue working normally as the buildworld runs, if your hardware is robust enough; while the build consumes system resources, it won't take any of your attention.

When the buildworld finishes, confirm that it completed without errors. If the build ends with a bunch of messages like those you see during a failed kernel compile, do not proceed with the upgrade. If you can't figure out why the build failed, go to Chapter 1 to see how you can get help. Never attempt to install a damaged or incomplete upgrade.

# **PARALLEL MAKE WORLD**

Experienced sysadmins have probably used the `-j` flag of `make(1)` to increase build speed. This starts multiple build