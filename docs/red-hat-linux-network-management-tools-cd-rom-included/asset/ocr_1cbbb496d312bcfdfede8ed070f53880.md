ble, destination, source, type, data, and checksum information. However, **ethereal** only reports the `Destination field`, `Source field`, and `Type` fields. The other fields are not displayed because the low-level Ethernet driver doesn't make the information available.

The remaining section includes the `ARP portion`, which in general denotes the higher-level protocols that have been encapsulated within the data portion of the Ethernet frame. As previously indicated, many higher-level protocols—like `TCP`, `IP`, and `IPX`—can be encapsulated in a frame just like `ARP`. In this case, the `ARP packet` includes information specific to the `ARP protocol`—hardware type, hardware address information, ARP packet type, sender's hardware address information, and target (desired) hardware address. We can determine that this packet is a `ARP request` because the `opcode field` is set to `1` (or `0x0001`) and the `Target hardware address` is `null` (or `00:00:00:00:00:00`).

The bottom panel contains the hexadecimal format of the packet displayed in rows and columns. As the user accesses each of the fields in the middle panel, the bytes that represent this data are highlighted in this bottom panel. For instance, when the user selects the `Ethernet Source` field of the packet, the following will be displayed:

```
```
0000  ff ff ff ff 00 60 97 0e a3 06 08 06 00 01
................................
0010  08 00 06 04 00 01 00 60 97 0e a3 06 0a 00 02 0a
................................
0020  00 00 00 00 00 00 0a 00 02 c9 02 c9 c9 c9 02 c9
................................
0030  02 c9 02 c9 02 c9 c9 02 c9 02 c9 02 c9
```

```

As indicated, the set of values `00 60 97 0e a3 06` is shown in bold to represent the sender's `datalink address` of this packet. The data in this panel is very useful because it provides a quick conversion to the low-level format, which can be used to identify network traffic patterns. The hexadecimal format is nearly universal when representing packets at this level. In the last chapter, we showed how to use `tcpdump` to scan for a specific string within a packet. The