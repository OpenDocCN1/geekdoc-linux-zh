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
```

These functions are called via the `ppc_md` structure and contain the machine- or platform-specific variants of these functions. You can see that some of these functions are machine specific and come from `mpc52xx_*` variants of the functions. Examples of these include `mpc52xx_restart` and `mpc52xx_map_io`. Others are specific to the hardware platform. Examples of platform-specific routines include `lite5200_map_irq` and `lite5200_setup_arch`.

# ## 16.4 Putting It All Together

Now that we have a reference from which to proceed, we can create the necessary files and functions for our own custom board. We copy the Lite5200 platform files for our baseline and modify them for our custom PowerPC platform. We'll call our new platform *PowerDNA*. The steps we will perform for this custom port are as follows:

+   1. Add a new configuration option to `.../arch/ppc/Kconfig`.
+   2. Copy `lite5200.*` to `powerdna.*` as a baseline.
+   3. Edit new `powerdna.*` files as appropriate for our platform.
+   4. Edit `.../arch/ppc/Makefile` to conditionally include `powerdna.o`.
+   5. Compile, load, and debug!

You learned how to add a configuration option to Kconfig in Chapter 4. The configuration option for our new PowerDNA port is detailed in Listing 16-11.