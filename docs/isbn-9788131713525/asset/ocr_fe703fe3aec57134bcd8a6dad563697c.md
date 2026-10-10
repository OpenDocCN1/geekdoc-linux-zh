16.3.3 Machine-Dependent Calls
Many common routines that the kernel needs either for initialization or for operation are architecture and machine (CPU) dependent. From the platform_init() function reproduced in Listing 16-8, we saw the following:

```
```
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
```

Lines similar to these make up the rest of the platform_init() function. Here the bulk of the platform-specific needs be communicated to the Linux kernel. The global variable ppc_md, of type struct machdep_calls, provides the hooks to easily customize the Linux kernel for a PowerPC platform. This variable is declared in.../arch/ppc/kernel/setup.c. Many places in the PowerPC-specific kernel branch call functions indirectly through this structure. For example, Listing 16-10 reproduces a portion of .../arch/ppc/kernel/setup.c, which contains support for the restart, power-off, and halt functions:

# ### Listing 16-10
### Generic PowerPC Machine Functions

```
```
void machine_restart(char *cmd)
{
#ifndef CONFIG_NVRAM
nram_sync();
#endif
ppc_md.restart(cmd);
}
```
```