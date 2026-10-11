# Floppy

80486 and earlier motherboards often placed floppy ports on expansion cards—often on the same cards that contained serial and parallel ports, or sometimes on a card with a SCSI host adapter. Modern motherboards, however, invariably include a floppy port, as shown in Figure 2.13. As with parallel and serial ports, floppy controllers are very well standardized, and don't vary much in modern computers. Most x86 computers today use 1.44MB floppy disks, but most controllers are capable of handling 2.88MB floppy drives. These higher-capacity floppies never caught on and are quite rare today.

![](bbox=[0.2, 0.32, 0.75, 0.52])

FIGURE 2.13
*One pin is missing from the floppy and each IIDE connector shown here. This is normal, and prevents backward insertion of the connecting cables, if they're properly keyed.*

NOTE
Some computers ship with an LS-120 disk rather than a conventional floppy disk. These disks are available in ElDE and SCSI versions, and can read and write both conventional 1.44MB floppy disks and special 120MB disks. On a system with an LS-120 disk instead of a regular floppy disk, the motherboard's floppy disk controller will go unused unless the system also contains a 5.25-inch floppy drive or a floppy-interfaced tape unit.

# ElDE

Next to the floppy port on most modern motherboards is a pair of EIDE ports (refer to Figure 2.13). Of the ports that are standard on modern motherboards, the EIDE ports are the most variable in design, and they're the only ports that benefit from specialized Linux drivers. These