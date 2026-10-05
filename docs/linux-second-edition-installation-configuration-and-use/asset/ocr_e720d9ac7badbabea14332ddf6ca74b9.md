# RECOMPILING THE KERNEL 205

If the patch file is present in uncompressed form, the patch command is:

```
root# patch -p1 < patch-2.2.31
```

With the following command, you can undo a patch:

```
root# patch -R -p1 < patch-2.2.31
```

Kernel patches always apply to the official kernel code released by Linus Torvalds. Many distributions, however, use modified kernels into which unofficial patches have been built in. Before you modify any kernel code yourself by means of a patch, you should always make sure that you have a correct basis from which to start.

Information on the current kernel code and a collection of unofficial patches which confer additional functionality to the kernel (but which have not yet been fully tested or are not generally desired) can be found at the following addresses:

```
http://www.linuxhq.com/
http://www.linuxxama.com/
```

# Configuring the kernel

Before you can compile the kernel, you must edit the .config file in the /usr/src/linux directory by entering all options that apply to the new kernel (which SCSI card, which Ethernet card, which network functions, and so on). .config is not edited manually, but by means of a special program which is started via make. Since kernel version 2.0, three different variations of this program have been available (You must choose one of the three variants listed below).

```
root# cd /usr/src/linux
root# make config
root# make menuconfig or
root# make xconfig
```

make config is the least variant. You must answer an endless list of questions one after the other. The advantage of this variation is that there is no need to install any additional program.\make menuconfig is much easier to handle: the configuration is still carried out in text mode, but it is possible to change a single point very quickly without having to repeat all other settings, make menuconfig only works if the library containing the necessary screen control functions is installed.\make xconfig is even more sophisticated: this variation only runs under X and only if Tel/Tk is installed. The configuration is now carried out via mouse clicks and in a very well-designed program.

NOTE

Independently of the variation you choose, you will still have to answer a number of questions about the kernel configuration. Do not rely on seemingly reasonable-default settings — even though they are all right with many options. If you have any