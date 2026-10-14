| Variable | Values / Meaning |
|---|---|
| `{x}` | `a, b, ..., n` 1st to 8th hard disk<br>`a` master on 1st IDE controller<br>`b` slave on 1st IDE controller<br>`c` master on 2nd IDE controller<br>`d` slave on 2nd IDE controller<br>etc. |
| `{trouble}` | `noprobe` — if probing for a new hard disk causes any problems<br>`none` — ignore CMOS entry and do not probe<br>`nowerr` — ignore the `WRERR_STAT` bit<br>`cdrom` — if the device was wrongly detected as a hard disk or if booting fails completely<br>`autotune` — use the fastest PIO mode<br>`slow` — to insert a long pause after each seek operation, which makes the device operate very slowly, but sometimes might help as a last resort |

The driver supports up to six IDE interfaces and, according to the ATA 2 specification, two devices can be connected to each of these.

To tell the kernel you have an ATAPI CD-ROM drive connected as master to the 2nd IDE controller, pass the parameter `hdc=cdrom`. Also see `/usr/src/linux/Documentation/ide.txt`.

*Example:* `hdd=cdrom`

+   - *Hard Disk*

`hd(x)=(cylinders),(heads),(sectors)[,(write)][,(irq)]`

| Variable | Values / Meaning |
|---|---|
| `{x}` | `a, b, ..., n` 1 to 8. Hard Disk |
| `{cylinders}` | number of cylinders |
| `{heads}` | number of heads |
| `{sectors}` | number of sectors |
| `{write}` | cylinders after which write compensation is used |
| `{irq}` | interrupt |

If the BIOS is an old one, it is possible that the geometry of the hard drive is not recognized correctly. The correct parameters will then be passed on so the kernel can still access the complete hard disk.