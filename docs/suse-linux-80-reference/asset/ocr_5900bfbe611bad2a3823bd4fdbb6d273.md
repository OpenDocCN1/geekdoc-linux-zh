+   - *Cabletron E21xx network card*

Name of module: `e2100.o`

| Parameter | Value |
|---|---|
| io | `{addr}` |
| irq | `{irq}` |
| mem | `{addr}` |
| xcvr | 0: internal; 1: external |

*Example:* `modprobe e2100 io=0x300 irq=10 mem=0xd000 xcvr=0`

+   - *Digital DE425 / 434 / 435 / 450 / 500 network cards*

Name of module: `de4x5.o`

`io=0x(bus)(device ID)`

| Parameter | Value |
|---|---|
| bus | number of the PCI bus, usually 0 |
| device ID | number of the PCI device |

With newer PCI BIOSes, these files are displayed when the machine boots.
In Linux, they can be seen with the same command `cat /proc/pci`.

*Example:* `modprobe de4x5 io=0x007`

+   - *Digital DEPCA / DE10x / DE20(012) / DE42, EtherWORKS network cards*

Name of module: `depca.o`

| Parameter | Value |
|---|---|
| io | `{addr}` |
| irq | `{irq}` |
| mem | `{mem}` |
| adapter_name | `{name}` e.g. DEPCA, de100, de101, de200, de201, de202, de210, de422 |

*Example:* `modprobe depca io=0x300 irq=10`

+   - *EtherWORKS 3 (DE203, DE204, DE205) network card*

Name of module: `ewrk3.o`