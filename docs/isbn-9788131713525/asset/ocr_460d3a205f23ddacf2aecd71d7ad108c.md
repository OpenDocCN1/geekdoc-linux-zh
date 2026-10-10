Notice two new configuration options related to your Vega and Constellation hardware platforms. As illustrated in Figure 4-4, you selected support for Vega; in the .config file, you can see the new CONFIG_option representing that the Vega board is selected and set to the value 'y'. Notice also that the CONFIG_option related to Constellation is present but not selected.

# 4.3.6 Kernel Makefiles

When building the kernel, the Makefiles scan the configuration and decide what subdirectories to descend into and what source files to compile for a given configuration. To complete the example of adding support for two custom hardware platforms, Vega and Constellation, let's look at the makefile that would read this configuration and take some action based on customizations.

Because you're dealing with hardware specific options in this example, assume that the customizations are represented by two hardware-setup modules called vega_setup.c and constellation_setup.c. We've placed these C source files in the .../arch/arm/mach-ixp4xx subdirectory of the kernel source tree. Listing 4-12 contains the complete makefile for this directory from a recent Linux release.

# Listing 4-12

Makefile from .../arch/arm/mach-ixp4xx Kernel Subdirectory

```
# Makefile for the linux kernel.
#
obj-y  += common.o common-pci.o
obj-$$(CONFIG_ARCH_IXDP4XX)  += ixdp425-pci.o ixdp425-setup.o
obj-$$(CONFIG_MACH_IXDPG425)  += ixp4g425-pci.o coyote-setup.o
obj-$$(CONFIG_MACH_ADL_COYOTE)  += coyote-pci.o coyote-setup.o
obj-$$(CONFIG_MACH_GTWX5715)  += gtwx5715-pci.o gtwx5715-setup.o
```

You might be surprised by the simplicity of this makefile. Much work has gone into the development of the kernel build system for just this reason. For the average developer who simply needs to add support for his custom hardware, the design of the kernel build system makes these kinds of customizations very straightforward.10

10 In actuality, the kernel build system is very complicated, but most of the complexity is cleverly hidden from the average developer. As a result, it is relatively easy to add, modify, or delete configurations without having to be an expert.