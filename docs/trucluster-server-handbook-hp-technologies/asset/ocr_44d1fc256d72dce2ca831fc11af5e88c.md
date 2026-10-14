Given that we know how our network is configured, we make the appropriate network mode changes from Twisted-Pair (the default setting) to 100 MB Full Duplex.

```
P00>>>show eia0_mode
eia0_mode          Twisted-Pair
```

```
P00>>>set eia0_mode fastfd
Changing to selected mode.
```

```
P00>>>show eia0_mode
eia0_mode          FastFD (Full Duplex)
```

For more information on what settings to use for your own network configuration, please refer to your switch or hub manufacturer's reference documentation, the hardware documentation for your AlphaServer system(s), and the hardware documentation for the NIC card that you will be using.

# 4.5.1.3 Verify the Memory Channel Interconnect Hardware

Finally, if we are using Memory Channel as the cluster interconnect hardware, we need to verify it and its firmware revision.

```
P00>>>show config
...
  Bus 00 Slot 08: DEC PCI MC      mca0.0.0.8.0        Rev: 22, mca0
```

This shows that we are using MC2 with firmware revision 0x22 (module revision 34). This satisfies the cluster interconnect hardware requirement and the firmware requirement for MC2.

+   - MC1 - Module Revision 11
+   - MC1.5 - 14
+   - MC2 - 32 or greater

| Module Revision | >>> show config |
|---|---|
| 11 | DEC PCI MC Rev: b, mc0a |
| Slot | Option Name | Type | Rev | Name |
| 2 | DEC PCI MC | 181011 | 000K | mc0 |
| 3 | DEC PCI MC | 181011 | 000K | mc1 |
| Bus 00 Slot 08: DEC PCI MC mca0.0.0.8.0 Rev: 20, mca0 |

# 4.5.2 Verify the Firmware

Although we updated the Alpha Firmware in section 4.3.1, let's verify the updated firmware.

```
P00>>> show version
version          V6.1-2 Oct 15 2001 13:36:04
```