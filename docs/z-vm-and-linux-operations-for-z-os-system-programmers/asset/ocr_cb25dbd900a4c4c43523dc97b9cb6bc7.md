# Removing a TDISK

You remove a TDISK in the same way you would remove most other virtual devices, by using the DETACH command; see Example 5-38. As its only parameter, this command takes the virtual device number of the device to detach.

# Example 5-38 Removing a TDISK

```
DETACH 9FF
DASD 09FF DETACHED
```

# Virtual DASD (VDISK)

A VDISK is a virtual DASD pack that resides in the z/VM system’s main storage instead of on a real DASD. This is exactly like the concept of a RAM disk that you might be familiar with from other operating systems. Because they exist in storage, VDISKs tend to be significantly faster than normal DASD devices, and also significantly smaller because it takes main storage away from system use.

# Important:

+   - A VDISK exists exclusively in storage and is not backed by a real disk. This means that when you log off or the system fails, your VDISK is destroyed and the data is lost. A VDISK is meant to be a temporary storage space.
+   - Do not store the only copy of important data on a VDISK.

z/OS hint: VDISKs are similar to using VIO type unit definitions in z/OS.

# Creating a VDisk

Not all z/VM installations allow the creation of VDISKs. This might be the case for your installation if the system administrator has not set up the system for VDISK allocation, or if free memory is too scarce.

However, you can request a VDISK allocation by using the DEFINE VFB-512 command. VFB-512 is an acronym for Virtual Fixed Blocks of 512 bytes.

Note that the DEFINE VFB-512 command takes two parameters: the virtual device number you want to assign to the new disk, and the size of this disk in 512-byte blocks. So, if you want a VDISK at device number 8FF that is 16 MB in size, use the command shown in Example 5-39 on page 265.