stale. The activation process may take some time as all extents of the stale volume(s) will have to be copied from the non-stale volume.

**MWC**: If this policy is selected, then for any write request to proceed on a mirrored volume, a request is passed to the MWC layer of the driver. An entry must be made to an MWC structure and copied to one of the volume group's physical volumes before it may continue through to the next LVM layer. If a resynchronization is required, all track groups represented by an active entry in the disk-based copies of the cache data must be synchronized. Activation here proceeds more quickly than with NOMWC since only LGT's with incomplete MWC entries will need to be synchronized. The performance hit here lies with the requirement that the MWC be written to disk before LVM advances the request through its various work queues.

Note that while all mirrors should be identical following resynchronization, there is no way to know which mirror had the most current data. The mirror chosen to be copied to the others is selected by random choice.

The MWC data on a physical disk is stored in the *mwc_entry* structure we examined earlier in this chapter and is sized to hold 126 individual entries (as of HP-UX 11i). There is also a kernel-based copy of this information (see Figure 11-9).

![](bbox=[0.22, 0.51, 0.82, 0.73])

# Figure 11-9 Mirror Write Consistency Records

Listing 11.13 is an extracted portion of a **listing (with annotation) created using q4> fields struct volgrp.**

# Listing 11.13 q4> fields struct volgrp

```
This contains the spinlock structure for controlling mp-access
to this data
72 0 4 0 * vg_ca_intlock.lvc_slock
```