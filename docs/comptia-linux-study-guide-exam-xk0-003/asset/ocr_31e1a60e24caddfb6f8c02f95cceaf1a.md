TABLE 7.10 Vital Statistics for Common Backup Devices

| Device | Cost of Drive | Cost of Media | Uncompressed Capacity | Speed | Access Type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Tape | $200–$4,000 | $0.15–$1.00/GB | 24–800GB | 1–120MB/s | Sequential |
| Hard disks | $10–$100 (for removable mounting kit or external enclosure) | $0.15–$0.50/GB (including mounting frame) | 80–2000GB | 20–100MB/s | Random |
| Optical discs | $25–$350 | $0.04–$0.50/GB | 650MB–50GB | 1–72MB/s | Random |

The types of devices that appear in Table 7.10 are those most often used for completely backing up Linux systems. Removable disks (such as USB flash drives or Zip disks) are often used for backing up a few files. Tapes are the traditional backup medium of choice, since they’ve historically been inexpensive on a per-gigabyte basis. Hard disks and optical discs are now cost-competitive with tape, though. Removable hard disks may provide greater capacity and convenience. These drives may be installed either in special internal drive frames that permit easy swapping or in external drive enclosures that plug into the computer via SCSI, FireWire, or USB ports. Optical discs, depending on the exact format used (CD-R, recordable DVD, or Blu-ray), may be even less expensive but are somewhat lacking in capacity compared to hard disks or tapes.

You may want to design a backup system that uses multiple backup types. For instance, you might perform full backups to a removable hard disk and then perform daily incremental backups onto optical discs. Such a plan can take advantage of the best features of each backup medium.

> If you restrict computers’ main installation partitions to about 8GB, those entire partitions will most likely fit, when compressed, on standard single-layer recordable DVDs. This can simplify backup and recovery efforts.

It’s generally wise to keep multiple backups and to store some of them away from the computers they’re meant to protect. Such off-site storage protects your data in case of fire, vandalism, or other major physical traumas. Keeping several backups makes it more likely you’ll be able to recover something, even if it’s an older backup, should your most recent backup medium fail.

If you decide to use hard disks in removable mounts as a backup medium, you’ll need ordinary internal drives and mounting hardware. The hardware comes in two parts: a mounting bay that fits in the computer and a frame in which you mount the hard drive. To use the