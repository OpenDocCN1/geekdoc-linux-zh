```
4 2 0 1 u_int pde_rtrap
```

The dirty bit is set to indicate that the page's content in cache has been modified and is not in sync with its memory-resident copy.

```
4 3 0 1 u_int pde_dirty
```

```
4 4 0 1 u_int pde_dbrk
```

The access rights consist of a 7-bit field and have the following translation:

+   0x00 PDE_AR_KR kernel read-only  
+   0x10 PDE_AR_KRW kernel read-write  
+   0x20 PDE_AR_KRX, PDE_AR_KXR kernel read-execute, kernel read-only  
+   0x30 PDE_AR_KRWX, PDE_AR_KXRW kernel read-write-execute  
+   0x6f PDE_AR_UX user read-only  
+   0x7f PDE_AR_UX user execute-only  
+   0xf PDE_AR_URW user read-write  
+   0x2f PDE_AR_URX, PDE_AR_URXKR, PDE_AR_CWX user read-execute, kernel read-only, and copy-on-write  
+   0x3f PDE_AR_UWRX user read-write-execute  
+   0x4c PDE_AR_GATE promote on execute-only (gateaway page)  
+   0x73 PDE_AR_NOACC no access allowed

```
4 5 0 7 u_int pde_ar
```

Next we can mark uncacheable pages

```
5 4 0 1 u_int pde_uncache
```

The protection ID is a pseudorandom number between 0 and 32767. A bitmap is maintained to keep track of which values are in use (protid_map). If a unique protection ID cannot be found, the kernel will panic!

```
5 5 2 2 u_int pde_protid
```

The execute bit is part of the stingy cache flush algorithm

```
7 7 0 1 u_int pde_executed
```

The first bit of the third word is used to indicate when an update to the pde data is in progress (this alleviates the necessity of using a spin-lock during hashtable updates) while the physical page number occupies the next 20 bits

```
8 0 0 1 u_int pde_uip
```

```
8 7 2 4 u_int pde_phys
```

The modified bit is used to let the kernel know the page's contents have been modified since the last time it was written to the back store (swap space)

```
11 4 0 1 u_int pde_modified
```

The trickle and block bits facilitate operations on specific PA-RISC processors with hardware walkers and block TLB entries (only available on a limited number of older 32-bit processors)

```
11 5 0 1 u_int pde_ref_trickle
```

```
11 6 0 1 u_int pde_block_mapped
```

If the alias bit is set, this structure was created as a result of a virtual page aliasing