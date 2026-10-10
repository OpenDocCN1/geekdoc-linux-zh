# **LISTING 16.3** Some of the Device Drivers Built into the GENERIC Kernel

```
# PCI Ethernet NICs that use the common MII bus controller code.
# NOTE: Be sure to keep the 'device mibus' line in order to use these NICs!
device  mibus  # MII bus support
device  dc  # DEC/Intel 21143 and various workalikes
device  fxp  # Intel EtherExpress PRO/100B (82557, 82558)
device  pcn  # AMD Am79C97x PCI 10/100 NICs
device  rl  # RealTek 8129/8139
device  sf  # Adaptec AIC-6915 ('Starfire')
device  sis  # Silicon Integrated Systems SiS 900/SiS 7016
device  ste  # Sundance ST201 (D-Link DFE-550TX)
device  tl  # Texas Instruments ThunderLAN
device  tx  # SMC EtherPower II (83c170 'EPIC')
device  vr  # VIA Rhine, Rhine II
device  wb  # Winbond W89C840F
device  xl  # 3Com 3c90x ('Boomerang', 'Cyclone')
```

# ## Device Hints

FreeBSD operates using the Device Filesystem (DEVFS) and *device hints*, which provide a way of abstracting the attributes of various devices so that the system can find them without needing the attributes to be compiled statically into the kernel. These attributes used to be defined like this, in the kernel config file itself:

```
device  ata0  at isa? port IO_WD1 irq 14
device  ata1  at isa? port IO_WD2 irq 15
```

Now, however, the kernel configuration file only needs to have this line:

```
device  ata
```

This change happened because the ata device has its attributes in the `/boot/device.hints` file, which is consulted by the kernel at boot time. Here are the relevant lines for this example:

```
hint.ata.0.at="isa"
hint.ata.0.port="0x1F0"
hint.ata.0.irq="14"
hint.ata.1.at="isa"
hint.ata.1.port="0x170"
hint.ata.1.irq="15"
```

With these attributes kept in a central location, the kernel knows on what bus, memory address, and IRQ (interrupt request) to find the ata device. Also, you can change these