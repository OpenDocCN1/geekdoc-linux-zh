It is always recommended that the package set that ships with the distribution be adhered to as long as is humanly possible. The assembly of packages on the CD is tested as a set, proven to work as a set, and is to be used as a set unless a serious need arises to break away and download updates. So be forewarned that although little risk is involved in performing an upgrade of any of these packages if you follow the directions, you are altering a tested, proven system; when you do so, you run the risk of having something not work exactly as it did before.

# ## UPGRADING pcmcia-cs

The pcmcia-cs (PCMCIA Card Services) package is very special. If you upgrade your kernel, the pcmcia-cs modules installed with your distribution might not work. The modules that compose this package need to be compiled against the kernel sources for the kernel you are running. You can wait for your distribution to release a new kernel binary package and the pcmcia-cs package that goes with it, or you can do the upgrade to both the kernel and pcmcia-cs package yourself.

With the new 2.4.x series kernel, many pcmcia modules are being built into the kernel, but not all are available. It is anticipated that this will change during the life of the 2.4.x kernels, but until it does, these instructions are necessary for those drivers not supported directly in the kernel.

The pcmcia-cs package offers drivers for PCMCIA chipsets and hardware (Ethernet cards, SCSI controllers, and modems), mostly for laptop systems. It also offers support for CardBus if it is compiled to do so.

One primary source of confusion with this package is the fact that it is composed entirely of modules, and therefore is not affected by the use of special boot parameters. So entering

```
ether=11,0x340,0,0,eth0
```

as a parameter when booting Linux does not pass any behavior altering information to the modules in the pcmcia-cs package (details on boot parameters and LILO are offered in Chapter 12, “Boot Loaders.”)

In fact, regular module parameters that are passed in the manner that was detailed earlier in this chapter do not work either. The pcmcia-cs package uses its own set of configuration files for its modules, so in essence it is an island among these sets of modules. However, adjusting how the modules load and passing parameters to those modules are not overly complex tasks after you know where to look and what to edit.

The main distribution site for the pcmcia-cs package is located at

```
ftp://sourceforge.org/pcmcia
```

There you can find the most recent version of pcmcia-cs, pointers to configuration information for hardware that is not included in the default configuration files, and developer versions of the package. (These are not for production systems—they are for testing purposes only.) Extensive documentation also is included at that site in the form of the PCMCIA-HOWTO and the PCMCIA-PROG documents. (The latter is intended for programmers.)

![](bbox=[0.94, 0.56, 1.0, 0.68])