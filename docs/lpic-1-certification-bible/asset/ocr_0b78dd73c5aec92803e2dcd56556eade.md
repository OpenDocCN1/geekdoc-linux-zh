patching file `linux/net/sunrpc/sunrpc_syms.c`  
patching file `linux/net/sunrpc/svc.c`  
patching file `linux/net/sunrpc/svcssock.c`  
patching file `linux/net/sunrpc/sysctl.c`  
patching file `linux/net/sunrpc/xdr.c`  
patching file `linux/net/sunrpc/xprt.c`  
patching file `linux/net/unix/af_unix.c`  
patching file `linux/net/unix/garbage.c`  
patching file `linux/net/x25/af_x25.c`  
patching file `linux/net/x25/x25_dev.c`  
patching file `linux/net/x25/x25_out.c`  
patching file `linux/scripts/Lindent`  
patching file `linux/scripts/ksymoops/ksymoops.c`  
patching file `linux/scripts/kw`  
patching file `linux/scripts/mkdep.c`

Either cat or zcat the patch file to the patch -p0 command, depending on if the file is compressed with gzip or not.

# ## Adding features with patches

Occasionally you may need a feature not supplied in the standard kernel distribution. Many times enhancements can be added to the kernel using a patch, similar to the patches in the previous section. These are written for specific kernel versions and should be used only with the correct kernel source. They are applied the same way as other patches. The following is an example.

```
```
debian:/usr/src# zcat linux-2.2.18-reiserfs-3.5.29-patch.gz |
patch -p0
patching file `linux/Documentation/Configure.help`
patching file `linux/fs/Config.in`
patching file `linux/afs/Makefile`
patching file `linux/fs/buffer.c`
patching file `linux/fs/fileystems.c`
patching file `linux/fs/inode.c`
patching file `linux/fs/reiserfs/Makefile`
patching file `linux/fs/reiserfs/README`
patching file `linux/fs/reiserfs/bitmap.c`
patching file `linux/fs/reiserfs/buffer.c`
patching file `linux/fs/reiserfs/buffer2.c`
patching file `linux/fs/reiserfs/dir.c`
patching file `linux/fs/reiserfs/do_balan.c`
patching file `linux/fs/reiserfs/file.c`
patching file `linux/fs/reiserfs/fh_mode.c`
patching file `linux/fs/reiserfs/hashes.c`
patching file `linux/fs/reiserfs/inode.c`
patching file `linux/fs/reiserfs/ioctl.c`
patching file `linux/fs/reiserfs/journal.c`
patching file `linux/fs/reiserfs/lbalance.c`
patching file `linux/fs/reiserfs/nameni.c`
...
```
```