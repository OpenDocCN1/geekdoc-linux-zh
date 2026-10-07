+   - _KERNEL_ — This tells the header files that this code will be run in kernel mode, not as part of a user process.

+   - MODULE — This tells the header files to give the appropriate definitions for a kernel module.

+   - LINUX — Technically speaking, this is not necessary. However, if you ever want to write a serious kernel module which will compile on more than one operating system, this will allow you to do conditional compilation on the parts which are OS dependant.

There are other symbols which have to be included, or not, depending on the flags the kernel was compiled with. If you're not sure how the kernel was compiled, look it up in /usr/include/linux/config.h

+   - _SMP_ — Symmetrical MultiProcessing. This has to be defined if the kernel was compiled to support symmetrical multiprocessing (even if it's running on one CPU). If you use Symmetrical MultiProcessing, there are other things you need to do (see chapter 12).

+   - CONFIG_MODVERSIONS — If CONFIG_MODVERSIONS was enabled, you need to have it defined when compiling the kernel module and to include /usr/include/linux/modversions.h. This can also be done by the code itself.

# Makefile

# Makefile for a basic kernel module

```
CC=gcc
MODCFLAGS :=-Wall -DMODULE -D__KERNEL__ -DLUX

hello.o: hello.c /usr/include/linux/version.h
	$(CC) $(MODCFLAGS) -c hello.c
	echo insmod hello.o to turn it on
	echo rmmod hello to turn it off
	echo
	echo X and kernel programming do not mix.
```