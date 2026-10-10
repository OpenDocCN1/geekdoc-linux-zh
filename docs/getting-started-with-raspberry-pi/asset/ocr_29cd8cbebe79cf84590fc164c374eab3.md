# **Listing 6.1. USB_UART Driver for the Linux Cell Phone**

```
Code View:

```
#include <linux/console.h>
#include <linux/platform_device.h>
#include <linux/tty.h>
#include <linux/tty_flip.h>
#include <linux/serial_core.h>
#include <linux/serial.h>
#include <asm/irq.h>
#include <asm/io.h>

#define USB_UART_MAJOR    200   /* You've to get this assigned */
#define USB_UART_MINOR_START 70   /* Start minor numbering here */
#define USB_UART_PORTS    2     /* The phone has 2 USB_UARTs */
#define PORT_USB_UART     30    /* UART type. Add this to
                                  include/linux/serial_core.h */

/* Each USB_UART has a 3-byte register set consisting of
   UU_STATUS_REGISTER at offset 0, UU_READ_DATA_REGISTER at
   offset 1, and UU_WRITE_DATA_REGISTER at offset 2 as shown
   in Table 6.1 */
#define USB_UART1_BASE    0xe8000000 /* Memory base for USB_UART1 */
#define USB_UART2_BASE    0xe9000000 /* Memory base for USB_UART2 */
#define USB_UART_REGISTER_SPACE 0x3

/* Semantics of bits in the status register */
#define USB_UART_TX_FULL  0x20   /* TX FIFO is full */
#define USB_UART_RX_EMPTY 0x10   /* TX FIFO is empty */
#define USB_UART_STATUS   0x0F   /* Parity/frame/overruns? */

#define USB_UART1_IRQ     3      /* USB_UART1 IRQ */
#define USB_UART2_IRQ     4      /* USB_UART2 IRQ */
#define USB_UART_FIFO_SIZE 32   /* FIFO size */
#define USB_UART_CLK_FREQ 16000000

static struct uart_port usb_uart_port[]; /* Defined later on */

/* Write a character to the USB_UART port */
static void
usb_uart_putc(struct uart_port *port, unsigned char c)
{
    /* Wait until there is space in the TX FIFO of the USB_UART.
       Sense this by looking at the USB_UART_TX_FULL bit in the
       status register */
    while (__raw_readb(port->membase) & USB_UART_TX_FULL);

    /* Write the character to the data port*/
    __raw_writeb(c, (port->membase+1));
}

/* Read a character from the USB_UART */
static unsigned char
usb_uart_getc(struct uart_port *port)
{
    /* Wait until data is available in the RX FIFO */
    while (__raw_readb(port->membase) & USB_UART_RX_EMPTY);

    /* Obtain the data */
```

```