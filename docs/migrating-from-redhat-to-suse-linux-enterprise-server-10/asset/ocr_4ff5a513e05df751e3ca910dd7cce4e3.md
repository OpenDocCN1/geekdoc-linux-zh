The configuration options are the same as those accessed by selecting LVM in the YaST Expert Partitioner.

> For additional information on configuring LVM, see the LVM HOWTO at http://tldp.org/HOWTO/LVM-HOWTO/.

# ## Configure LVM with Command Line Tools

Setting up LVM consists of several steps, with a dedicated tool for each:

+   - Tools to Administer Physical Volumes  
+   - Tools to Administer Volume Groups  
+   - Tools to Administer Logical Volumes

This is just a brief overview, not all available LVM tools are covered. To view the tools that come with LVM, enter  
`rpm -ql vm2 | less` on a command line, and have a look at the corresponding manual pages for details on each of them.

# ### Tools to Administer Physical Volumes

Partitions or entire disks can serve as physical volumes for LVM.

The ID of a partition used as part of LVM should be **Linux LVM, 0x8e**. However the ID **0x83, Linux**, works as well.

To use an entire disk as physical volume, it may not contain a partition table. Overwrite any existing partition table with `dd`:

```
da10:~ # dd if=/dev/zero of=/dev/hdd bs=512 count=1
```