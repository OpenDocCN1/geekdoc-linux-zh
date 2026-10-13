# Your Kernel Is Too Large and Too Slow

If your kernel is too large and too slow, you probably have compiled too many options and drivers into your kernel. To solve this problem, you need to reconfigure your kernel to include the minimum options and drivers needed. You can check memory and swap usage by your kernel by viewing the contents of `/proc/meminfo`.

# You Have Problems with Your Parallel Port or Printer

Printer device naming was changed in kernel 2.1. What used to be `lp1` is now `lp0` under the new kernel. Looking through system logs will help you track down what device names are being used.

When configuring the kernel, make sure you configured parallel port support and PC style hardware under `General Setup`. You must also configure parallel printer support under `Character devices`.

# You Have Problems with Your CD-ROM Drive

Many people have problems with IDE/ATAPI CD-ROM drives. If your CD-ROM drive is the only drive on an IDE interface, be sure that it is jumpered to be the master drive.

If your CD-ROM drive is connected to your sound card’s IDE interface, you may have trouble and may find that the drive will work better when connected to your computer’s main IDE interface.