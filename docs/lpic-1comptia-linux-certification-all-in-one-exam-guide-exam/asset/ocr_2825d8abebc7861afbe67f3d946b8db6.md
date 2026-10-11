*   **modules** Contains a list of all the kernel modules currently being used by the system. A sample is shown here:

    ```
    fuse 75897 3 - Live 0xffffffffa01c0000
    p6t_LOG 5898 8 - Live 0xffffffffa02f0000
    xt_tcpudp 2859 10 - Live 0xffffffffa01f0000
    xt_pkttype 1288 3 - Live 0xffffffffa01e3000
    ipt_LOG 6067 8 - Live 0xffffffffa00f7000
    xt_limit 2559 16 - Live 0xffffffffa00d0000
    mvsyn 4288 0 - Live 0xffffffffa0082000
    wrmblock 13824 1 - Live 0xffffffffa0065000
    ... 
    ```

+   *   **version** Contains the information about the version of the Linux kernel running on the system
+   *   **/scsi/** Contains files that contain information about the SCSI devices in your system if you're using a SCSI adapter
+   *   **/bus/devices** Contains information about the USB devices in the system
+   *   **/ide/** Contains files that contain information about the IDE devices in your system

In addition to /proc, the /sys/ directory also provides information about the hardware installed in the system. The file system is organized in a tree structure grouped by the hardware bus, the hardware device, and their associated drivers. The top level of the /sys/ directory contains many subdirectories, including

+   *   **/sys/block** Contains a symbolic link file for each block device in the system
+   *   **/sys/bus** Contains a directory for each data bus in the system, including the ISA, PCI, SCSI, and USB busses

Each bus directory has two subdirectories: devices and drivers, as shown here:

```
```bash
wsl: /sys/bus/scsi # ls
devices drivers drivers_autoprobe drivers_probe uevent
```
```

The devices subdirectory contains entries for every device on that bus, while the drivers directory contains subdirectories for each driver loaded for a device on this bus.

+   *   **/sys/class** Contains all device classes available
+   *   **/sys/devices** Contains an entry for every discovered device
+   *   **/sys/module** Contains subdirectories for each module loaded into the kernel, as shown next:

```
```text
wsl: /sys/module # ls
6250      acpi
ac97_bus  acpi_apm
ata_generic ata_pix
        ip6t_LOG
        ip6t_REJECT
        ip6table_filter
        ip6table_mangle
        ip6table_raw
        ip_tables
        ipt_LOG

nf_conntrack_ipv6
nf_conntrack_netbios_ns
nf_defrag_ipv4
parport
parport_pc
pci_hotplug
pcie_aspm

snd_seq
snd_seq_device
snd_seq_midi
snd_seq_midi_event
snd_timer
soundcore
spurious
```
```