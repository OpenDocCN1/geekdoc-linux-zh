o, the vSphere environment is ready. The hosts are loaded, storage is provisioned, and vCenter Server is ready to go. Now it's time to create some virtual machines. This chapter focuses on creating virtual machines, starting with basic background on the PowerShell New-VM cmdlet. You'll discover the various methods of creating virtual machines. Then we'll take a deep dive into the vSphere API, and you'll learn the dark art of using advanced methods and techniques. Finally, you'll learn to use custom attributes as well as VMware Tools installation.

# # Use the New-VM Cmdlet

The New-VM cmdlet is used to add, create, clone, or register a new virtual machine (VM). It has grown up over the past six versions of PowerShell and is quite powerful. It is not, however, complete, and there are still things that cannot be done natively within PowerShell. A good analogy for using PowerShell cmdlets is like speaking a foreign language. For the most part, the words are the same, but they're often said in a different order. If the vSphere web console is your native lang then otherwise, the New-VM cmdlet will always create a VM with the specifications listed in Table 6.1.

TABLE 6.1 PowerShell New-VM default values

| Parameter | Default value |
|---|-|
| DiskGB | 4 |
| DiskStorageFormat | Thick |
| GuestId | winXPProGuest |
| MemoryMB | 256 |
| NumCpu | 1 |
| Version | 11 |

Based on VMware vSphere PowerShellCLI 6.0 build 2442775

> NOTE Some of the defaults are inherited from the vSphere host. For instance, a vSphere 5.5 host connected to a vCenter 6.0 instance would assume VM version 10. Likewise, if an NFS datastore is used the disk storage format will be.