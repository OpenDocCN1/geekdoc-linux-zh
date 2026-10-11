# Table 9.1 Common Varieties of SCSI

| SCSI Type | Speed | Cable Type | Maximum Cable Length in Meters |
| --- | --- | --- | --- |
| SCSI-1 | 5MB/s | 25- or 50-pin | 6m |
| SCSI-2 | 5MB/s | 50-pin | 6m |
| Fast SCSI-2 | 10MB/s | 50-pin | 3m |
| Fast/Wide SCSI-2 | 20MB/s | 68-pin | 3m |
| Ultra SCSI | 20MB/s | 50-pin | 3m or 1.5m¹ |
| UltraWide SCSI | 40MB/s | 68-pin | 3m or 1.5m¹ |
| Ultra2 Wide SCSI (LVD) | 80MB/s | 68-pin | 12m |
| Ultra3 Wide SCSI (LVD) | 160MB/s | 68-pin | 12m |

¹Maximum cable length is 3m for three or fewer devices, 1.5m for more than three devices.

One important characteristic of SCSI is that each variety is compatible with those that came before it. (One exception is HVD, which is incompatible with other SCSI signaling methods.) You can use a Fast SCSI-2 or even a SCSI-1 device on the latest host adapters supporting Ultra3 SCSI, for instance. In the case of 50- and 68-pin devices, either your host adapter must support both interfaces, or you must use an adapter to connect a 50-pin device to a 68-pin host adapter.

# ### SCSI-1

SCSI-1 was the original SCSI standard. Approved in 1986 but used on some systems earlier than that, SCSI-1 was capable of 5MB/s speeds using 25- or 50-pin cables. As I mentioned earlier, however, 25-pin cables are not recommended. A normal 50-pin SCSI cable includes a large number of separate ground wires, but to reduce the number of pins, a 25-pin cable combines these all into one pin. The resulting cable usually works, but is less reliable than a 50-pin cable, particularly as the cable length grows. Today, few devices are limited to SCSI-1 speeds.

# ### SCSI-2 and Fast SCSI-2

At its core, SCSI-2 is largely a clarification and extension of SCSI-1 protocols. The original SCSI-1 addressed the needs of hard disks but little else. Manufacturers found the SCSI bus appealing for CD-ROM drives, tape backup drives, and other devices, however, and so the manufacturers improved, using proprietary extensions to the SCSI-1 protocol. Many of these were adopted for the SCSI-2 standard, and future devices followed the new standard.