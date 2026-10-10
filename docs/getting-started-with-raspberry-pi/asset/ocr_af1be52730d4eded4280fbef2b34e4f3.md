```
```
timeout 5    #5 second to alter boot_order or parameters

title kernel 2.6.23    #Boot Option 1
#The boot image resides in the first partition of the first disk
#under the /boot/ directory and is named vmlinuz-2.6.23. 'ro'
#indicates that the root partition should be mounted read-only.
kernel (hd0,0)/boot/vmlinuz-2.6.23 ro root=/dev/hda1

#Look under section "Freeing initrd memory:387k freed"
initrd (hd0,0)/boot/initrd
```
```

Command-line arguments affect the code path traversed during boot. As a simple example, assume that the command-line argument of interest is called *bootmode*. If this parameter is set to *1*, you would like to print some debug messages during boot and switch to a runlevel of *3* at the end of the boot. (Wait until the boot messages are printed out by the init process to learn the semantics of runlevels.) If *bootmode* is instead set to *0*, you would prefer the boot to be relatively laconic, and the runlevel set to *2*. Because you are already familiar with *init/main.c*, let's add the following modification to it:

```
```c
Code View:
static unsigned int bootmode = 1;
static int __init
is_bootmode_setup(char *str)
{
  get_option(&strstr, &bootmode);
  return 1;
}

/* Handle parameter  "bootmode=" */
__setup("bootmode=", is_bootmode_setup);

if (bootmode) {
  /* Print verbose output */
  /* ... */
}

/* ... */

/* If bootmode is 1, choose an init runlevel of 3, else
   switch to a run level of 2 */
if (bootmode) {
  argv_init[++args] = "3";
} else {
  argv_init[++args] = "2";
}

/* ... */
```
```

Rebuild the kernel as you did earlier and try out the change. We discuss more about kernel command-line arguments in the section "Memory Layout" in Chapter 18, "Embedding Linux."