# # Dump Device

Like the log screens, the System Dump menu (see Figure 8-7) is critical to managing problem information. By default, AIX 4.3 and 5L use the `/dev/hd6` paging space as the primary dump device. In most large environments, a dedicated dump device should be defined, other than paging space. In previous releases, there was a problem with systems that had mirrored paging space and in which a dump occurred. In a kernel panic, confusion arose about which *side* of the mirror to use as the dump device. This problem has been corrected in AIX 4.3.3 with ML 6. However, the main reason for a dedicated dump device is to allow an automatic reboot after a system dump that preserves the dump image without having to save it to a tape or disabling a paging device.

Access the SMIT dump menu with the SMIT FastPath **smit dump**.

```
`# smit dump`
```

![](bbox=[0.15, 0.43, 0.81, 0.86])

**Figure 8-7.** System Dump SMIT panel