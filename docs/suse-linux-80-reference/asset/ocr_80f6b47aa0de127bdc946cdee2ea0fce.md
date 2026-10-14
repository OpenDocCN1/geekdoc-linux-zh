+   - *Sony CDU 31/33 A*

Name of module: `cdu31a.o`

| Parameter | Value |
|---|---|
| cdu31a_port | *(addr)* |
| cdu31a_irq | *(irq)* |

*Example:* `modprobe cdu31a cdu31a_port=0x300 cdu31a_irq=10`

+   - *Sony CDU 535*

Name of module: `sonycd535.o`

| Parameter | Value |
|---|---|
| sonycd535 | *(addr)* |

*Example:* `modprobe sonycd535 sonycd535=0x300`

+   - *Soundblaster Pro 16 MultiCD*

Name of module: `sbpcd.o`

`sbpcd={addr},{type}`

`{type}` can have the following values:

| Variable | Values / Meaning |
|---|---|
| 0 | LaserMate |
| 1 | SoundBlaster |
| 2 | SoundScape |
| 3 | Teac16bit |

*Example:* `modprobe sbpcd sbpcd=0x300,0`

# The Parallel Port

The operation of the parallel port is somewhat complex. After configuration, a complete subsystem is available.

+   - *Parallel port*

Name of module: `parport.o`

*Example:* `modprobe parport`

+   - *Parallel port — architecture-specific*

Name of module: `parport_pc.o`