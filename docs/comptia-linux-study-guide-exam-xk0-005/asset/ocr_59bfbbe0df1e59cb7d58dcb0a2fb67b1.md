data on your system's processor(s), memory, NIC(s), USB controller(s), disk(s), and so on. It is typically installed by default on most distributions or available in a standard repository (Chapter 13 covered installing software packages).

Two helpful options are `-short`, which produces a nice table-formatted hardware data display, and `-businfo`, which shows information associated with SCSI, USB, IDE, and PCI devices. An example of using the `-short` option is shown snipped in Listing 24.15.

# **Listing 24.15:** Using the `-short` option with the `lshw` command

```
# lshw -short
```

|H/W path | Device | Class | Description |
| :--- | :--- | :--- | :--- |
| /0 | | system | VirtualBox |
| /0 | | bus | VirtualBox |
| /0/0 | | memory | 128KiB BIOS |
| /0/1 | | memory | 4GiB System memory |
| /0/2 | | processor | Intel(R) Core(TM) [...] |
| /0/100 | | bridge | 440FX - 82441FX PMC [Natoma] |
| /0/100/1 | | bridge | 82371SB PIIX3 ISA [Natoma/Triton II] |
| /0/100/1.1 | scsi1 | storage | 82371AB/EB/MB PIIX4 IDE |
| /0/100/1.1/0.0.0 | /dev/cdrom | disk | CD-ROM |
| /0/100/2 | | display | VirtualBox Graphics Adapter |
| /0/100/3 | enp0s3 | network | 82540EM Gigabit Ethernet Controller |
| /0/100/4 | | generic | VirtualBox Guest Service |
| /0/100/5 | | multimedia | 82801AA AC '97 Audio Controller |
| /0/100/6 | | bus | KeyLargo/Intrepid USB |
| /0/100/6/1 | usb1 | bus | OHCI PCI host controller |
| /0/100/7 | | bridge | 82371AB/EB/MB PIIX4 ACPI |
| /0/100/8 | enp0s8 | network | 82540EM Gigabit Ethernet Controller |
| /0/100/9 | scsi1 | storage | 82801H/HM (ICH8M/ICH8M-E) SATA [...] |
| /0/100/9/0/0 | /dev/sda | disk | 16GB VBOX HARDDISK |
| /0/100/9/0/1 | | volume | 1GiB Linux filesystem partition |
| /0/100/9/0/2 | /dev/sda2 | volume | 13GiB Linux LVM Physical Volume partition |
| [...] | | | |
| /0/4 | | input | PnP device PNP0f03 |
| /1 | virbr0-nic | network | Ethernet interface |
| [...] | | | |

You can also employ the `-c`lass option with the `lshw` utility. This option provides detailed information about a particular hardware component. The different classes available are displayed in the `lshw -short` command's output. A snipped example of using the `-c`lass option is shown in Listing 24.16.