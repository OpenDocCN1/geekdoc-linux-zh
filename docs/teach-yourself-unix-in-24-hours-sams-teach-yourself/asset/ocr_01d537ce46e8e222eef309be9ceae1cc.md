# Looking into Files

core: core from getty
gendynix: SYMMETRY i386 stand alone executable not
-stripped version 1
tftboot: symbolic link to /usr/tftboot

This example is from a Sequent computer running DYNIX, the Sequents' version of UNIX, based on Berkeley 4.3 BSD with some AT&T System extensions. It's the same machine that has problems identifying mail folders.

Executable binaries are explained in detail by the file command boot is SYMMETRY i386 stand alone executable version 1. The specifics aren't until to: The most important word to see in this output is executable, indicating that the file is the result of compiling a program. The format SYMMETRY i386, version 1, and the file requires no libraries or other files to execute—it's stand-alone.

For gendynix, the format is similar, but one snippet of information is added that isn't indicated for boot: The executable file has been stripped.

![](bbox=[0.238, 0.458, 0.807, 0.507])

![](bbox=[0.13, 0.445, 0.23, 0.511])

When a program dies unexpectedly in UNIX, the operating system tries to leave a snapshot of the memory that the program was using, to aid in debugging. Wading through these files can be difficult—it's usually reserved for a few experts at each site, where there is still some useful information inside. The best, simplest, is to check it with the file command. You can see in the preceding listing that file recognized the file as a crashed program memory image and further extracted the name of the program that originally failed, getty, causing the program to fail. When this failure happens, UNIX creates an image of the program in memory at the time of failure, which is called a core dump.

The fourth of the listings offers an easy way to understand symbolic links, indicated in is -CF output with the special suffix #, in the preceding example with tftboot*. Using file, you can see that the file tftboot in the root directory is actually a symbolic link to a file with the same name elsewhere in the file system,/usr/tftboot.

There are differences in output formats on different machines. The following example shows what the same command would generate on a Sun Microsystems workstation, examining analogous files:

```
% file boot core kadb tamp
boot: sparc executable
core: core file from "popper"
```

![](bbox=[0.865, 0.806, 0.99, 0.893])