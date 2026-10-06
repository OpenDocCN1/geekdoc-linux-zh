# Chapter 28 ♦ Emulation and Virtualization 701

This creates a virtual disk called `test.disk`

Then you can run an operating system installation either from a real CD or from a CD image. Example:

```
qemu -hda test.disk -cdrom /dev/hdc -monitor stdio -boot d -m 192
```

This will start QEMU with the virtual hard disk (-hda), and using the real CD drive (-cdrom /dev/hdc). The option -boot -d makes the virtual system boot from CD (think of drive D), and a m 192 makes 192MB of memory. The extra option -monitor stdio provides a command-line monitor interface that you can use to interact with QEMU from the outside. You need this option if you are installing an operating system from more than one CD, you need it to force QEMU to change disks.

After the operating system has been installed into QEMU, you can run it with a command similar to the following:

```
qemu -hda test.disk -monitor stdio -boot c -m 192
```

Here -boot c makes the system boot from hard disk (think of drive C):

Figure 28-5 shows a Windows 2000 installation under QEMU.

![](bbox=[0.181, 0.536, 0.626, 0.749])

**Figure 28-5**: Installing Windows 2000 Professional under QEMU

# Building and Using the QEMU Accelerator

If you want to use the QEMU accelerator, you will need to download the source distribution of QEMU and the source for the `kqemu` module. First unpack the source distribution somewhere:

```
tar xzvf qemu-0.7.1.tar.gz
```