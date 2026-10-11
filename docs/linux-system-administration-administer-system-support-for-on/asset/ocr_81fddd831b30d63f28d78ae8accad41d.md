```
boot = /dev/hda
#compact # faster, but won't work on all systems.
# delay = 5
vga = normal # force sane state
# ramdisk = 0 # paranoia setting
# End LILO global section
# Linux bootable partition config begins
image = /zImage
    root = /dev/hda1
    label = linux
    read-only # Non-UMSDOS file systems should be mounted read-only for checking
# Linux bootable partition config ends
For added insurance, run the command lilo at the root prompt.
# illo
Added linux *
```

Now reboot. If you are running a computer with standard equipment (not a lap-top), you shouldn't have problems. Also keep in mind that running a develop-mental Linux kernel can give you similar problems that you might have on a laptop.

If you are recompiling a kernel on a laptop, make sure are you using the most up-to-date drivers available. You may have to download some Internet; however, it will save you a lot of grief in the future. For example, I was running out of date PCMCIA drivers on my laptop and noticed that my Ethernet card worked but my modem didn't. I needed to check the versions of the drivers and find the most recent ones. I found that updating drivers meant better hardware support, including increased performance.

# # Troubleshooting Your Kernel

If you have a kernel that won't compile, you might get a message like this:

```
sb_common.c: At top level:
sb_common.c:266: warning: `sb16_set_mpu_port' defined but not used
make[2]: *** [sb_common.o] Error 1
make[2]: Leaving directory `/usr/src/linux-2.0.33/drivers/sound'
make[1]: *** [subdirs] Error 2
make[1]: Leaving directory `/usr/src/linux-2.0.33/drivers'
make: *** [linuxsubdirs] Error 2
```