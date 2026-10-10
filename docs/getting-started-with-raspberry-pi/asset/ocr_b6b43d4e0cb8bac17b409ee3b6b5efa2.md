# ## Consistent Checksums

Because of legal issues latent in distributing the kernel, companies often ship kernel modifications to customers in the form of a source patch generated against an agreed-upon base. Customers, in turn, integrate the patch into an in-house code repository and build the software locally.

Comparing the MD5 checksum of your binary images with that of your customer’s is a guard against patching errors, but the values may not match as-is because the kernel and module images often contain information specific to the build environment. To force identical MD5 sums, exclude such data while generating kernel and module images at either end. Here are some typical scenarios that inject environmental data into the object image:

+   • Some driver methods toss a call to `BUG()` to announce conditions that are never supposed to occur. `BUG()` spits out, among other things, the offending filename and line number. The pathname of the file depends on the location of your build sandbox. It gets imprinted in the produced image and contributes to MD5 variance. For example, look at `nfs_unlock_request()` in `fs/nfs/pagelist.c`:

```
```
void
nfs_unlock_request(struct nfs_page *req)
{
    if (!NFS_WBACK_BUSY(req)) {
        printk(KERN_ERR "NFS: Invalid unlock attempted\n");
        BUG();
    }
    /* ... */
}
```
```

`BUG()` is defined in `include/asm-your-arch/bug.h`:

```
```
#define BUG() do {
__asm__ __volatile__ ("ud2\n"
:: "i" (__LINE__), "i" (__FILE__))
... 
```
```

You can compile `BUG()` away by disabling `CONFIG_BUG` during kernel configuration. Or you may get rid of the line number and filename information emitted by `BUG()` by switching off `CONFIG_DEBUG_BUGVERBOSE`.

+   • The wd33c93 driver (`drivers/scsi/wd33c93.c`) announces the time of compilation during initialization. You will find this snippet if you go to the end of the initialization routine, `wd33c93_init()`:

```
```
void
wd33c93_init(struct Scsi_Host *instance,
const wd33c93_regs regs, dma_setup_t setup,
dma_stop_t stop, int clock_freq)
{
/* ... */
printk("	Version %s - %s, Compiled %s at %s\n",
WD33C93_VERSION, WD33C93_DATE, __DATE__, __TIME__);
}
```
```

The build timestamp thus gets embedded inside the image, causing the MD5 checksum to depend on it.