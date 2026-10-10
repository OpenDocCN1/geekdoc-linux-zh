
First, we search for a special tag that identifies the data structure as a struct `bi_record`. If that is found, the `bootinfo` pointer is set to the address of the start of the `bootinfo` records. From there, the records are parsed and the hardware related data is gathered. This can be seen by inspecting `.../arch/ppc/kernel/setup.c`. Currently, `bi_records` can contain the kernel command line, the start and end address of the `initrd` image, the machine type, and the size of the memory. Of course, you can extend this for your own requirements.

If no `bi_record` data is found, the PowerPC architecture expects this data in the form of U-Boot board information structure, or `bd_info`. It is the bootloader's responsibility to construct this data structure and pass the address in register `r3`. Currently, many bits of hardware information are available in the `bd_info` structure, including information on DRAM, FLASH, SRAM, processor clock rates, bus frequencies, serial port baud rate setting, and more.

The `bi_record` structure can be examined in `.../include/asm-ppc/bootinfo.h`, and the `bd_info` structure can be found in `.../include/asm-ppc/ppcboot.h`.

It is the responsibility of the platform-initialization routines to make use of any of the data that might be necessary to complete the hardware setup, or to communicate it to the kernel. For example, `plat_form_init()` sets up a pointer to a function whose name reveals its purpose. The code from Listing 16-8 is reproduced here:

```c
ppc_md.find_end_of_memory = mpc52xx_find_end_of_memory;
```

Looking at the function `mpc52xx_find_end_of_memory()`, which is found in `.../arch/ppc/syslib/mpc52xx_setup.c`, we find the following:

```c
u32 ramsz1e = _res.bi_memsize;

if (ramsize == 0) {
 ... /* Find it another way */
}

return ramsz1e;
```

The `_res` data structure above is the board information structure, whose address was passed to us from the bootloader in register `r3` above. As you can see, the generic setup code stored the *residual* data (as it is often called) passed in by the bootloader, but it's up to the machine or platform-specific code to make use of it.

### 16.3.3 Machine-Dependent Calls

Many common routines that the kernel needs either for initialization or for operation are architecture and machine (CPU) dependent. From the `platform_init()` function reproduced in Listing 16-8, we saw the following:

```c
/* Setup the ppc_md struct */
ppc_md.setup_arch    = lite5200_setup_arch;
ppc_md.show_cpuinfo   = lite5200_show_cpuinfo;
ppc_md.show_percpuinfo   = NULL;
ppc_md.init_IRQ       = mpc52xx_init_irq;
ppc_md.get_irq       = mpc52xx_get_irq;

#ifndef CONFIG_PCI
ppc_md.pci_map_irq    = lite5200_map_irq;
#endif

ppc_md.find_end_of_memory = mpc52xx_find_end_of_memory;
ppc_md.setup_io_mappings  = mpc52xx_map_io;

ppc_md.restart    = mpc52xx_restart;
ppc_md.power_off  = mpc52xx_power_off;
ppc_md.halt        = mpc52xx_halt;
```

Lines similar to these make up the rest of the `platform_init()` function. Here the bulk of the platform-specific needs be communicated to the Linux kernel. The global variable `ppc_md`, of type `struct machdep_calls`, provides the hooks to easily customize the Linux kernel for a PowerPC platform. This variable is declared in `.../arch/ppc/kernel/setup.c`. Many places in the PowerPC-specific kernel branch call functions indirectly through this structure. For example, Listing 16-10 reproduces a portion of `.../arch/ppc/kernel/setup.c`, which contains support for the restart, power-off, and halt functions:

#### Listing 16-10
Generic PowerPC Machine Functions

```c
void machine_restart(char *cmd)
{
#ifndef CONFIG_NVRAM
nram_sync();
#endif
ppc_md.restart(cmd);
}
```

```c
void machine_power_off(void)
{
#ifdef CONFIG_NVRAM
    nvram_sync();
#endif
    ppc_md.power_off();
}

void machine_halt(void)
{
#ifdef CONFIG_NVRAM
    nvram_sync();
#endif
    ppc_md.halt();
}
```

These functions are called via the `ppc_md` structure and contain the machine- or platform-specific variants of these functions. You can see that some of these functions are machine specific and come from `mpc52xx_*` variants of the functions. Examples of these include `mpc52xx_restart` and `mpc52xx_map_io`. Others are specific to the hardware platform. Examples of platform-specific routines include `lite5200_map_irq` and `lite5200_setup_arch`.

## 16.4 Putting It All Together

Now that we have a reference from which to proceed, we can create the necessary files and functions for our own custom board. We copy the Lite5200 platform files for our baseline and modify them for our custom PowerPC platform. We'll call our new platform *PowerDNA*. The steps we will perform for this custom port are as follows:

- 1. Add a new configuration option to `.../arch/ppc/Kconfig`.
- 2. Copy `lite5200.*` to `powerdna.*` as a baseline.
- 3. Edit new `powerdna.*` files as appropriate for our platform.
- 4. Edit `.../arch/ppc/Makefile` to conditionally include `powerdna.o`.
- 5. Compile, load, and debug!

You learned how to add a configuration option to Kconfig in Chapter 4. The configuration option for our new PowerDNA port is detailed in Listing 16-11.

#### Listing 16-11
Configuration Option for PowerDNA

```
config POWERDNA
    bool "United Electronics Industries PowerDNA"
    select PPC_MPC52xx
    help
        Support for the UEI PowerDNA board
```

This Kconfig entry is added just below the entry for LITES200 because they are related. Figure 16-4 illustrates the results when the configuration utility is invoked.

![](img/7a1144833e62564667e7dd9eb4c9f03d_471_0.png)

**FIGURE 16-4**
Machine type option for PowerDNA

Notice that when the user selects POWERDNA, two important actions are performed:

- 1. The CONFIG_PPC_MPC52xx configuration option is automatically selected. This is accomplished by the select keyword in Listing 16-11.
- 2. A new configuration option, CONFIG_POWERDNA, is defined that will drive the configuration for our build.

> To preserve space, we temporarily removed many machine types in Figure 16-4 prior to LITES200.

The next step is to copy the files closest to our platform as the basis of our new platform-initialization files. We have already decided that the Lite5200 platform fits the bill. Copy `lite5200.c` to `powerdna.c`, and `lite5200.h` to `powerdna.h`. The difficult part comes next. Using the hardware specifications, schematics, and any other data you have on the hardware platform, edit the new `powerdna.*` files as appropriate for your hardware. Get the code to compile, and then proceed to boot and debug your new kernel. There is no shortcut here, nor any substitute for experience. It is the hard work of porting, but now at least you know where to start.

Many tips and techniques for kernel debugging are presented in Chapter 14, "Kernel Debugging Techniques."

To summarize our porting effort, Listing 16-12 details the files that have been added or modified to get Linux running on the PowerDNA board.

#### Listing 16-12
PowerDNA New or Modified Kernel Files

```text
linux-2.6.14/arch/ppc/configs/powerdna_defconfig
linux-2.6.14/arch/ppc/Kconfig
linux-2.6.14/arch/ppc/platforms/Makefile
linux-2.6.14/arch/ppc/platforms/powerdna.c
linux-2.6.14/arch/ppc/platforms/powerdna.h
linux-2.6.14/drivers/net/fec_mpc52xx/fec.c
linux-2.6.14/drivers/net/fec_mpc52xx/fec.h
linux-2.6.14/drivers/net/fec_mpc52xx/fec_phy.h
linux-2.6.14/include/asm-ppc/mpc52xx.h
```

The first file is the default configuration, which enables a quick kernel configuration based on defaults. It is enabled by invoking `make` as follows:

```text
$ make ARCH=ppc CROSS_COMPILE=<cross- prefix> powerdna_defconfig
```

We’ve already discussed the changes to the Kconfig file. Modification to the makefile is trivial—the purpose is to add support for the new kernel configuration based on `CONFIG_POWERDNA`. The change consists of adding a single line:

```text
obj-$(CONFIG_POWERDNA)		+= powerdna.o
```

The heart of the changes come in the `powerdna.{c,h}` files and changes to the FEC (Fast Ethernet Controller) layer. There are minor differences between `powerdna.c` and `lite5200.c`, the file from which it was derived. Two primary issues required changes. First, PCI was disabled because it is not used in the PowerDNA design. This required some minor tweaking. Second, the PowerDNA
