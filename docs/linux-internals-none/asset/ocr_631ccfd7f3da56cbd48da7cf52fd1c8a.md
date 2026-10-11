figured into the kernel. This procedure was called *hierarchical initialization* and worked fine for simple systems with a limited number of devices.

In 2.3.x the hardware recognition procedure changed considerably. Previously it was necessary to change the *init* callback of the higher layer to add something like:

```
```
#ifdef CONFIG_MY_DRIVER
    init_my_driver();
#endif
```
```

This is no longer necessary, because we include a pointer to *init_my_driver()* in a special ELF section, and the higher layer parses each special file (device driver) *init* section and recalls all the *init* callback without any need to write code outside the `.c` file of the low-level driver. This has simplified initialization at boot time.

It is interesting to note that, with this new hardware recognition strategy or sequence, the linking order at device driver compile time has become significant, because the information is in the ELF header of the objects. Consequently, special cases may still need explicit calling of the initialization function. For most cases, however, that's not necessary. The dynamic kernel structures in the early stage (for example, while setting up the console or the virtual memory manager) are allocated via a new *bootmem* allocator, which can return big chunks of physically contiguous memory. In 2.2.x we used to advance a pointer to keep track of the memory allocated by hand in the early stage, but with newer machines tables can be allocated in the middle of the memory; therefore an allocator (*bootmem*) was needed that was also aware of memory holes in the early stage of the boot process. The *bootmem* allocator also makes sure to return non-DMA memory when possible. This way, we avoid wasting the first 16MB of memory with kernel structures that don't need to be there.

Once the virtual memory manager is booted and initialized and *get_pages* and *get_free_pages* get the appropriate pointers from *bootmem*, all further allocations of memory are handled by the VM directly.

# ## Shutdown

All the hard work is done in user space. The *halt -f* only tells the *init* process that the machine will halt soon via a *SIGSTP*. Then, shutdown executes *sys_reboot(SYS_HALT)* and later will call *exit(2)* on an IA32