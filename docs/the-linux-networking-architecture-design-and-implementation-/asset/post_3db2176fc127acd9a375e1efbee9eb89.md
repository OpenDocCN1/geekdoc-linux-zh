
# CHAPTER 7
# The Serial-Line Internet Protocol (SLIP)

## 7.1 INTRODUCTION

The packet-oriented IP protocol is used to communicate over the Internet. However, a modem can transmit only a continuous byte stream. For this reason, to establish a connection from your local PC over an analog telephone line to the worldwide Internet, we need a protocol that encapsulates network packets so that they can be transmitted over a modem connection between a local computer and a point of presence (PoP). The two endpoints of the modem connection can then communicate over IP. The point of presence itself is directly connected to the Internet and routes IP packets between the local PC and the Internet. (See Figure 7-1).

Another possible use of such a protocol is for the IP communication of two computers over the V.24 interface, which is available in most PCs. This use lets you build an IP network at little cost (and very low speed) without the need to install additional interfaces, such as Ethernet cards.

RFC 1055 [Romk88] specifies the SLIP (Serial Line IP) for the V.24 task. SLIP represents an intermediate layer within the network architecture: At its upward face, packets are taken from or forwarded to the IP layer; at its downward face, data are to be received from a serial interface driver.

As compared with the more recent PPP protocol (see Chapter 8), SLIP is very simple, but offers a rather limited functionality:

- SLIP includes no mechanisms for establishment of a controlled connection: As soon as SLIP has started on both ends, the connection is implicitly established. For this reason, no parameters, such as IP address, DNS information, or the SLIP operating mode used, can be negotiated. These parameters have to be set manually or by use of a script before SLIP is started.

![](img/5a25b942ec3329b8799f2b5f0de564f6_156_0.png)

SLIP serves exclusively for the transmission of Version-4 IP packets. Other network protocols (e.g., IP version 6 or X.25) are not supported.
- SLIP has no mechanisms to detect or correct errors; these functions have to be handled by higher network layers.
- In contrast to PPP, the payload in transmitted IP packets cannot be compressed. The CSLIP operating mode (described in the next bullet) allows you to compress the IP packet headers only.

In addition to the standard operating mode, SLIP supports the following modes:

- In CSLIP (Compressed SLIP), the packet headers in transmitted IP packets are compressed by the Van–Jacobson algorithm to utilize slow modem connections

SLIP uses only printable ASCII characters for data transmission. This is necessary when the underlying modem connection cannot transmit all control characters of the ASCII alphabet—for example, because the XON and XOFF control characters are used for flow control. However, a maximum payload of 6 bits per character can be transmitted in this way, and so the transmission rate drops by one quarter.

### 7.1.1 Packet Detection and Character Stuffing

A serial interface or a modem connection is designed for the transmission of continuous sequences. To be able to send data packets of the IP protocol over such a connection, the sender has to insert special markings, which are then used by the receiver to detect the end of each packet. In SLIP, this is implemented so that the END control character (byte code 192) is inserted before and after each packet.

To ensure unique detection of packet boundaries, the END character must never occur inside a packet. Of course, this constraint is undesirable, because we want to be able to transmit arbitrary data packets transparently. To maintain this transparency, three additional control characters (ESC, ESC_END, and ESC_ ) are used to implement a so-called *character stuffing* (shown in Figure 7–2):

| IP packet | IP packet as byte sequence | SLIP byte stream |
|---|---|---|
| IP header | Byte 1 | END |
| | : | Byte 1 |
| TCP/UDP header | ESC | ESC |
| | : | ESC END |
| data | END | ESC |
| | | Byte n | END |

FIGURE 7–2
SLIP marks packet boundaries and uses character stuffing at the sender side.

TABLE 7–1 SLIP control characters.

| Character | Byte Code |
|---|---|
| END | 192 |
| ESC | 219 |
| ESC_END | 220 |
| ESC_ESC | 221 |

- Each occurrence of END in packet data is replaced by the ESC ESC_END string,
- Each occurrence of ESC in packet data is replaced by the ESC_END string.

The receiver can reverse character stuffing as follows to reconstruct the original IP packet:

- If the ESC character occurs, then the next character is ESC_ESC or ESC_END. In this case, the first ESC is deleted, and the second character is replaced by ESC or END.
- If the END character occurs, then this is the end of that packet, and the packet can be forwarded to the IP layer.

Table 7–1 lists the four control characters used by SLIP and their byte codes.

## 7.2 SLIP IMPLEMENTATION IN THE LINUX KERNEL

Before we describe the SLIP implementation in the Linux kernel, we will first discuss the concept of TTY devices and TTY line disciplines, the better to illustrate how SLIP is implemented in Linux. Subsequently, this section will give an overview of the most

### 7.2.1 TTY Devices and Line Disciplines

In Linux, all devices that act as terminals are grouped under TTY (Teletype or Terminal). A TTY device is a character device, and Table 7–2 shows examples.

TABLE 7–2 Examples of TTY devices.

| TTY device | Meaning |
|---|---|
| tty0 | virtual consoles |
| pty# | pseudo-terminals |
| ttyS | serial interfaces |

A TTY device can generally switch between different line disciplines. This means that, in the kernel, each TTY device has a line discipline, which is in charge for the input and output. Specifically, implementation of SLIP in the Linux kernel requires the driver to register a new TTY line discipline with the kernel to make it available.

![](img/5a25b942ec3329b8799f2b5f0de564f6_158_0.png)

FIGURE 7–3 Interplay between TTY line disciplines and TTY device.

The tty_ldisc structure includes a number of function pointers, which have to be set by the driver of the line discipline. The following code briefly explains the function pointers.

```c
tty_ldisc.h
struct tty_ldisc {
    int     magic;
    char    *name;
    int     num;
    int     flags;
    /* The following routines are called from above.  */
    int     (open)(struct tty_struct);
    void    (close)(struct tty_struct);
    void    (flush_buffer)(struct tty_struct);
    ssize_t (chars_in_buffer)(struct tty_struct);
    ssize_t (read)(struct tty_struct *tty, struct file *file, unsigned char *buf, size_t nr);
    ssize_t (write)(struct tty_struct *tty, struct file *file, const char *buf, size_t nr);
    int     (ioctl)(struct tty_struct *tty, struct file *file, unsigned int cmd, unsigned long arg);
    void    (set_termios)(struct tty_struct *tty, struct termios *old);
    unsigned int (poll)(struct tty_struct *, struct file *, struct poll_table_struct);

    /* The following routines are called from below.  */
    void    (receive_buf)(struct tty_struct *, const unsigned char *cp, char *fp, int count);
    int     (receive_room)(struct tty_struct);
    void    (write_wakeup)(struct tty_struct *);
};
```

The following functions are called from "above" (i.e., by the program or module accessing the TTY device):

The function open() is called as soon as the TTY device switches to this line discipline.

The function close() is called when the current TTY line discipline is deactivated. This happens when a TTY device switches from this line discipline into another
