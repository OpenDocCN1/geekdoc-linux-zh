# Installing Red Hat Linux

since you might need to reference it later. Add an entry to the Administrator's Logbook detailing the installation.

| Administrator's Logbook: Initial Installation |
| System: E12345678 |
| Action: Installed Red Hat Linux 7.0 |
| Installation Options: Basic server-class installation |
| Modifications: Added jed and joe editor packages |
| Hardware: |
| Video: ATI Xpert 98 (Mach 64, 8MB RAM) |
| Modem: External USR Sportster 56K Voice |
| Network Card: Linksys LNE100TX (PNIC Tulip Chipset) |
| CD-ROM Drive: Pioneer DVD-113 |
| Hard drives: Western Digital AC26400B 6.4GB & Maxtor 91000D 9.1GB |
| SCSI Card: Generic Symbios 53c860-based host adapter |
| SCSI Device: External Lega Zip-100 drive |
| Sound card: Integrated motherboard VIA 82c686a sound chip | |

How Things Work

PART 1

If you've purchased a Red Hat Official boxed set, it will include the image to create a boot diskette by CD-ROM installation like the one we perform. If your computer supports booting from a CD-ROM, you can boot directly from the Red Hat CD-ROM and will not need to create a boot disk. If it does not, or if you are installing from a different medium, you might have to create your own boot disk as described later in this chapter.

# Choosing a Partitioning Scheme

Disk partitioning is the division of the hard drive into logical parts that contain specific components of the operating system.

Although most people choose a more structured file system layout, Red Hat 7.0 requires only one Linux partition. Assuming its size is sufficient, this partition can contain both