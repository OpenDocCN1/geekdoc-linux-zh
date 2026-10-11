In addition to identification and priority control, each peripheral device needs its own working space in physical memory where it can communicate with other devices. This working space is identified by a hexadecimal number range representing a certain area of RAM and is referred to as an **Input/Output (I/O) address**. Many I/O addresses are commonly reserved for certain devices on a system, as listed in Table 7-3. As with IRQs, it is important to ensure that the I/O address of a device has not been assigned to another device, because neither device will function properly.

# Table 7-3  Default I/O address assignments

| I/O Address  | Device                         |
| ------------ | ------------------------------ |
| 3F8-3FF      | COM1                           |
| 2F8-2FF      | COM2                           |
| 3E8-3EF      | COM3                           |
| 2E8-2EF      | COM4                           |
| 378-37F      | LPT1                           |
| 278-27F      | LPT2                           |
| 000-01F      | DMA controller                 |
| 020-03F      | Primary interrupt controller   |
| 040-05F      | Timer                          |
| 060-06F      | Keyboard                       |
| 070-07F      | Real-time clock                |
| 0A0-0BF      | Secondary interrupt controller |
| 0F0-1F7      | Math coprocessor               |
| 1F0-1F7      | Hard disk                      |
| 3D0-3DF      | VGA                            |
| 3F0-3F7      | Floppy disk controller         |

![](bbox=[0.17, 0.83, 0.23, 0.88])

# NOTE

> At minimum, each device must have a unique IRQ and I/O address.