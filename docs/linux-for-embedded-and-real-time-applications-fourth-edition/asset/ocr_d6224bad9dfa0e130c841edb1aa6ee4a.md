U-boot began as a PowerPC boot loader named 8xxROM written by Magnus Damm. Wolfgang Denk subsequently moved the project to Source Forge, and renamed it PPCBoot. The source code was briefly forked into a product called ARMBoot by Sysgo GmbH. The name was changed to u-boot when the ARMBoot fork was merged back into the PPCBoot tree. Today, u-boot supports roughly a dozen architectures, and over 1000 different boards.

The development of u-boot is closely tied to Linux, with which it shares some header files. Some of the source code originated in the kernel source tree.

U-boot supports an extensive command set that not only facilitates booting, but also manages flash memory, downloads files over the network, and more. Appendix I details the command set. The command set is augmented by environment variables and a scripting language.

# Installing and Configuring U-Boot

The current version of u-boot is available from the following git repository:

```
git clone git://git.denx.de/u-boot.git
```

There is a very extensive README file in the top-level directory. There are additional README files in the doc/ directory that primarily describe features of specific boards.

There is also a patch to the mainline code for the BeagleBoard. Point your web browser to:

```
https://rcn-ee.com/repos/git/u-boot-patches/
```

and select the subfolder corresponding to the u-boot version you got from git. Download 0001-am335x_evm-uEnv,t-txtdoottz-n-fixes.patch to your u-boot directory. Then execute:

```
patch -p1 < 0001-am335x_evm-uEnv,t-txtdoottz-n-fixes.patch
```

In my case, two of the eight files failed their patches, but were pretty easy to patch by hand.

Current u-boot implementations support the same Kconfig configuration mechanism as the Linux kernel and BusyBox. Again, we have to start with a default configuration. The u-boot version I downloaded has _defconfigs for over a thousand boards. In our case it is:

```
make am335x_boneblack_defconfig
```

Follow that with:

```
make xconfig
```

Fig. 15.1 is the top-level xconfig menu for u-boot. This shows that the ARM (Advanced RISC Machines) architecture is selected along with the TI OMAP2 + variant. There is probably not a whole lot that you would want to change, other than which commands get included.