# ioscan

The ioscan command is useful for viewing the hardware configuration of a system. For disk resources, this includes the interface cards as well as the I/O devices. The command displays the hardware path to the hardware module, the class of the hardware module, and a brief description. This is good for tracking the system's disk configuration.

Listing 5-6 shows the output from the ioscan command; the -1 option generates a full listing.

# lvdIsplay

The lvdIsplay command can be used to get information for disk resource management. It displays Logical Volume Manager (LVM) logical volume configuration information and the logical volume status. Information about mirrored copies is included if you are using MirrorDisk/UX. Listing 5-7 shows the logical volume status and mirrored copies, among other information, in the output from lvdIsplay.

Listing 5-6 Output from the ioscan command showing information about hardware devices configured on a system.

```
# ioscan -f
```

```
Class H/W Path Driver S/W State H/W Type Description
```

```
===
```

```
bc 0 root CLAIMED BUS_NEXUS
```

```
bc 1 8 ccio CLAIMED BUS_NEXUS I/O Adapter
```

```
bc 2 8/0 bc CLAIMED BUS_NEXUS Bus Converter
```

```
tty 0 8/0/0 mux2 CLAIMED INTERFACE MUX
```

```
ext_bus 0 8/4 c720 CLAIMED INTERFACE GSC add-on F/W SCSI
```

```
target 0 8/4.5 tgt CLAIMED DEVICE
```

```
disk 0 8/4.5.0 sdisk CLAIMED DEVICE SEAGATE ST34572WC
```

```
target 1 8/4.6 tgt CLAIMED DEVICE
```

```
ctl1 4 8/4.6.0 sctl CLAIMED DEVICE Initiator
```

```
target 2 8/4.12 tgt CLAIMED DEVICE
```

```
disk 2 8/4.12.0 sdisk CLAIMED DEVICE SEAGATE ST32272WC
```

```
target 3 8/4.13 tgt CLAIMED DEVICE
```

```
disk 3 8/4.13.0 sdisk CLAIMED DEVICE SEAGATE ST32272WC
```

```
target 4 8/4.14 tgt CLAIMED DEVICE
```

```
disk 4 8/4.14.0 sdisk CLAIMED DEVICE SEAGATE ST32272WC
```

```
target 5 8/4.15 tgt CLAIMED DEVICE
```

```
disk 5 8/4.15.0 sdisk CLAIMED DEVICE SEAGATE ST32272WC
```