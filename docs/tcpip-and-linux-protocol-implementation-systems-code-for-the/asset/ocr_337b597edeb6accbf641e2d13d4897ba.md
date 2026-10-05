# 5.4.3 A Specific Device Driver–3c501

This is a 3Com Ethernet driver from Linux 2.4. This is a pretty old device, but it has enough intelligence to show some of the features of Linux. In fact, some of its limitations also mean that a driver for it must also exhibit some classic workarounds for well-known device problems—some device problems never go even in state-of-the-art hardware.

The _net_device_ structure illustrates how data is associated with the hardware-specifies of a network device, including bus interface and memory and interrupt priority, as well as external cards.

Basically, we are usually given an I/O address that a card is memory-mapped to, and then a given card has a number of registers for control and status—in this case there are all addresses we can read internal configuration back from the card (e.g., a manufacturer-assigned Ethernet, for example).

Figure 5.25 Ethernet driver-data: linux/net/3c501.c.

```
#define RX_STATUS (ioaddr + 0x06)
#define RX_CMD RX_STATUS
#define TX_STATUS (ioaddr + 0x07)
#define TX_CMD TX_STATUS
#define GP_LOW (ioaddr + 0x08)
#define GP_HIGH (ioaddr + 0x09)
#define RX_BUF_CLR (ioaddr + 0x0A)
#define RX_LOW (ioaddr + 0x0A)
#define RX_HIGH (ioaddr + 0x0B)
#define SAPROM (ioaddr + 0x0C)
#define AX_STATUS (ioaddr + 0x0E)
#define AX_CMD AX_STATUS
#define DATAPORT (ioaddr + 0x0F)
#define TX_RDT_STATUS /* /
#define EL1_DATAPTR 0x08
#define EL1_RXPTR 0x0A
#define EL1_SAPROM 0x0C
#define EL1_DATAPORT 0x0F
/* /
Writes to the ax command register.
#define AX_OFF 0x00 /* Irq off, buffer access on */
#define AX_STR 0x40 /* Load the buffer */
#define AX_KMIT 0x44 /* Transmit a packet */
#define AX_RX 0x48 /* Receive a packet */
#define AX_LOOP 0x0C /* Loopback mode */
#define AX_RESET 0x80
```