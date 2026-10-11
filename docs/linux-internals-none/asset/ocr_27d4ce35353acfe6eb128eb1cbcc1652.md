noinitrd

[RAM] Tells the kernel not to load any

configured initial RAM disk.

no-scroll

[VGA]

nosmp

[SMP] Tells an SMP kernel to act as a UP

kernel.

nosync

[Hw, M68K] Disables sync negotion for all

devices.

optcd=

[Hw,CD]

panic=

[KNL] Kernel behaviour on panic.

parport=0

[Hw,PPT] Specify parallel ports. 0 disables.

parport=auto

Use 'auto' to force the driver to use

any IRQ/DMA settings detected (the

[[IRQ,,DMA]]

default is to ignore detected IRQ/DMA settings

because of possible conflicts). You can

specify the base address, IRQ, and DMA

settings: IRQ and DMA should be numbers, or

'auto' (for using detected settings on that

particular port), or 'nofifo' (to avoid

using a FIFO even if it is detected).

Parallel ports are assigned in the order

they are specified on the command line,

starting with parport0.

pas16=

[Hw,SCSI]

pcbit=

[Hw,ISDN]

pcc.

[PARIDE]

pci=

[PCI]

pd.

[PARIDE]

pf.

[PARIDE]

pg.

[PARIDE]

pirq=

[SMP,APIC] mp-table.

plip=

[PPT,NET] Parallel port network link.

profile=

[KNL] enable kernel profiling via /proc/profile

(param:log level).

prompt_ramdisk=

[RAM] List of RAM disks to prompt for floppy

disk before loading.

pt.

[PARIDE]

ramdisk=

[RAM] Sizes of RAM disks in kilobytes

[deprecated].

ramdisk_size=

[RAM] New name for the ramdisk parameter.

ramdisk_start=

[RAM] Starting block of RAM disk image (so you

can place it after the kernel image on a

boot floppy).

reboot=

[BUGS=ix86]

reserve=

[KNL,BUGS] force the kernel to ignore some

iomem area.

riscom8=

[Hw,SERIAL]

ro

[KNL] Mount root device read-only on boot.

root=

[KNL] root filesystem.

rw

[KNL] Mount root device read-write on boot.

S

[KNL] run init in single mode.

sbpcd=

[Hw,CD] Soundblaster CD adapter.

scsi_logging=

[SCSI]

sjcd=

[Hw,CD]