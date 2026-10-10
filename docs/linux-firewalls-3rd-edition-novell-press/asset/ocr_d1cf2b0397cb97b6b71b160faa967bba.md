When you're ready to begin the actual build process, there are three primary commands used to build the kernel. Actually, for now, most likely four commands will be used because I'm going to assume that modules are included in the default kernel that you're building. Eventually, when you disable modules for added security, you won't have to run the final **make** command that I'll show because it's just used to build the modules.

The first build step generates the dependencies. From within the */usr/src/linux* directory, type the following:

```
```
make dep
```
```

This command should run relatively quickly. Continue the build process by typing this:

```
```
make clean
```
```

The **make clean** step is also somewhat fast, obviously depending on the available resources.
Finally, create the kernel itself by typing this:

```
```
make bzImage
```
```

The *bzImage* option compresses the kernel using *bzip2*. Another alternative used on systems without *bzip2* is **make zImage**, which uses *gzip* instead of *bzip2*. Because you have *bzip2* on this system (you had it in order to uncompress the kernel source), you can use **bzImage**.

The kernel will now compile. This process will take a varying amount of time depending on a couple factors. First and foremost, the speed of and load on the processor(s) and available RAM will be the biggest factors that will determine the amount of time that the kernel will take to compile. On a hardly used dual-Intel Xeon processor machine with 1GB RAM, the kernel takes less than five minutes to compile. On the other hand, an Intel Pentium 60 with 24MB RAM will take many hours to compile the kernel. The second factor in determining the amount of time a kernel takes to compile is the number of options you included with the kernel. Adding SMP code and many (possibly unnecessary) drivers will cause the compile time to increase.

Sit back and relax or go do something else while the kernel is compiling. Now is a good time to read the kernel HOWTO that I recommended earlier; that is, if you haven't already read it. Hopefully the kernel compile won't fail with an error, though this does sometimes happen. Usually it's due to a troublesome driver or a conflict between two drivers. You'll know that the compile failed if the kernel stops compiling and you're left with something like this on the screen:

```
```
Error 1
***[make]***
Error 2
```
```