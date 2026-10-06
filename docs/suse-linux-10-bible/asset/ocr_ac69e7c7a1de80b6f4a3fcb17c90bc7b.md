The configuration of the kernel that is actually running is always available in
/proc/config.gz, a gzipped virtual file in the /proc filesystem, which is created in
memory on the fly by the running kernel (see Listing 29-1).

# Listing 29-1: Looking at the Configuration of the Running Kernel

```
root@: /proc zcat config.gz | more
#
# Automatically generated make config: don't edit
#
CONFIG_X86=y
CONFIG_MMU=y
CONFIG_UID16=y
CONFIG_GENERIC_ISA_DMA=y

#
# Code maturity level options
#
CONFIG_EXPERIMENTAL=y
CONFIG_CLEAN_COMPILE=y
# CONFIG_STANDALONE is not set
CONFIG_BROKEN_ON_SMP=y

#
# General setup
...
```

When you get bored with reading this, type q to quit more.

It is instructive to page through this file and look at the various options in it that
refer to the hardware, filesystems, and so on that are to be supported by the kernel.

+   * The y=y at the end of lines means that the support for the relevant item is com- piled into the kernel.
* Lines ending not set clearly imply that the support is not included.
* Lines ending = m imply that the support is provided by a loadable kernel mod- u than being compiled into the kernel itself. SUSE provides most funct-ality in the form of modules.

In a newly installed system, you should find that /usr/src/limux/.config is identi- cal to /boot/config-<version-number>-default and to the content of /proc/con- fig.gz when uncompressed.