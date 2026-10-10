In Listing 16-3, we listed the functions in the `lite5200.c` platform-initialization file. Every function except `platform_init()` is declared as static. Therefore, as shown in Figure 16-3, this is the entry point for the platform-initialization file. The rest of the functions in the file are referenced only from within the file itself.

Let's examine the entry function `platform_init()`. Listing 16-8 reproduces the `platform_init()` function from the `lite5200.c` file.

# Listing 16-8

# Lite5200 platform_init Function

```
```
void __init
platform_init(unsigned long r3, unsigned long r4,
           unsigned long r5, unsigned long r6,
           unsigned long r7)
{
  /* Generic MPC52xx platform initialization */
  /* TODO Create one and move a max of stuff in it.
     Put this init in the syslib */

  struct bi_record *bootinfo = find_bootinfo();

  if (bootinfo)
    parse_bootinfo(bootinfo);
  else {
    /* Load the bd_t board info structure */
    if (r3)
      memcpy((void*)&__res, (void*)(r3+KERNELBASE),
             sizeof(bd_t));

    #ifdef CONFIG_BLK_DEV_INITRD
    /* Load the initrd */
    if (r4) {
      initrd_start = r4 + KERNELBASE;
      initrd_end = r5 + KERNELBASE;
    }
    #endif

    /* Load the command line */
    if (r6) {
      *(char *)r7+KERNELBASE) = 0;
      strcpy(cmd_line, (char *)(r6+KERNELBASE));
    }
  }

  /* PPC Sys identification */
  identify_ppc_sys_by_id(mfspr(SPRN_SVR));
}
```
```