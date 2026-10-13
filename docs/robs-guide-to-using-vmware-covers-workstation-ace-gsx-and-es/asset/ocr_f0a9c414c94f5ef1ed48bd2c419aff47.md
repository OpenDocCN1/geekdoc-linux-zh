![](bbox=[0.11, 0.1, 0.9, 0.56])

Figure 7.5: Locking a snapshot is only available in Workstation version 4.x and GSX Server 3.x.

+   7. Copy the .vmx file (and if important for your configuration, also the nvram bios file) to the directory for the second virtual machine.

8. You can now power both virtual machines on. They will both read from the shared master disk, but all changes to the disk will go into .REDO files which you will find in the virtual machine directory for each machine. This happens because the .REDO files do not have an absolute path; instead, they are stored in a path relative to the machine (the VM directory itself).

```
ide0:0.redo=".\Windows 2000 Professional.vmdk.REDO_a03292"
```

> Tip: If you use the configuration with a separate swap disk for your guest operating system (as described in section 9.1: “Performance tips”) in combination with this shared disk setup, then assign every virtual machine a separate swap disk and set the disk to be an independent. Keep the swap disk .vmdk file in the directory with the virtual machine configuration files. This way, the swap disk will not be affected by the snapshot. There is no need to keep the page file contents consistent between pre and post Snapshot configurations.

> Tip: Copying the virtual machines will make exact copies of everything in the operating system, including the identity, SID, computer name, IP address, etc. All