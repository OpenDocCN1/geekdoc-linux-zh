You must remember that you need to run the lilo command every time you modify the configuration file and every time you change a kernel image file, whether you modify the configuration file or not. Even if you store a new kernel image in the same place as the old one, and with the same name, you must still run the lilo command to have the new kernel installed.

# 7.4 Kernel Build

The Linux kernels supplied with most software distributions are configured to support as wide a range of hardware as possible, so that they will work with as many machines as possible for Linux installation purposes. Once you have an installation running, it is a good idea to build a custom kernel specifically for your machine. In general, this will reduce the size of the kernel and thus increase the amount of memory you have available in which to work. If you only have a limited amount of memory fitted in your machine (4 Mb for example), then this can make a noticeable difference.

Assuming that you have installed the Linux kernel sources and the GNU C/C++ compiler as part of your Linux installation, then building a new kernel is very straightforward.

The first task is to check that your installation of the Linux sources has created two symbolic links in the directory /usr/include, as in the following example:

```
# cd /usr/include
# ls -l asm linux
lrwxrwxrwx 1 root root 26 Jul 4 17:27 asm -> /usr/src/linux
/include/asm
lrwxrwxrwx 1 root root 28 Jul 4 17:27 linux -> /usr/src/lin
ux/include/linux
```

If the symbolic links already exist then you must not perform the next step. If they do not exist then you will need to set them up manually, probably to replace a pair of directories of the same name. These things can be done as follows:

```
# cd /usr/include
# rm -fr asm linux
# ln -s /usr/src/linux/include/asm asm
# ln -s /usr/src/linux/include/linux linux
```

# 7.4.1 Configuration

The next step is to choose which facilities and hardware drivers you want to include in your new kernel; you do this with the following commands: