to insert the ppa module into the kernel. (The "ppa" stands for, I guess, the "parallel port first interface "a" )

After everything is done, inspect /proc/modules to see if the ppa module is loaded (or run as root lsmod to list the modules). The information from kernelcfg goes to the file /etc/conf.modules so you have difficulty removing modules (e. inserted by mistake)--as I just--did edit and adjust this file manually.

Now your zipdrive should be recognized. Put a zipdisk in it and try mounting using the previously described command (as root):

```
mount -t vfat /dev/sda4 /mnt/zipdrive
```

Using the Linux kernel v2.2.0.36 and below, you will not be able to use a printer which is connected through the parallel port zip drive (this works with the kernel 2.2.x). Use the command

```
uname -a
see which version of kernel is running.
```

**RedHat 6.0 and 6.1** The zipdrive (zip100 drive) installation did not work during my upgrade to RedHat 6.0 (the installation program said that it couldn't find the zipdrive). So, after the installation was completed, I issued the following commands to insert the modules for parallel port zip drive into the kernel (as root):

```
/sbin/insmod parport
/sbin/insmod ppa
```

To have these two lines executed automatically after each reboot. I added them at the end of the file /etc/rc.d/rc.local (this file is something like autoec.bat on DOS).

If this still does not work for you, you may also want to edit the file /etc/conf.modules. Mine contains such a line:

```
alias parport_lowlevel parport_pc
```

and there is no line mentioning the "ppa" module.

For the newer Zip250 drive, I have the following two lines executed from my /etc/rc.d/rc.local file:

```
/sbin/insmod parport
/sbin/insmod imm
```