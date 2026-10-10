```
struct file_operations *fops)
{
    chrdevs[major].name = name;
    chrdevs[major].fops = fops;
    return 0;
}
```

When this function is called, the major number is connected to the file operations structure set up by the device driver. The call is made by the device driver in the `cq_init()` function. The only other task performed by `cq_init()` is the initialization of some of the values in `cq_area`. In order to get the call performed during boot time, a call to it may be placed in the mem.c program near the end near the call to lp_init(). The command

```
linuxbox$ mknod /dev/cq c 102 0
```

creates an entry in file system for the cq device, giving it a major number of 102 and a minor number of 0. This entry in the /dev directory is then used to translate references to /dev/cq into calls to the functions listed in the file operations structure.

# 11.4 Serial Port Digitizer Driver

The Sealex device is a hand-held measuring device for reading distances off of a flat surface. It inputs data at a rate of 600 baud through the serial port. Since it has no handshaking hardware it does not respond to software which treats it as a modem or a terminal. It also handles data in a special format which packs two four-bit characters into each byte sent or received. For both of these reasons it is useful to write a special driver for it.

One important element of a typical device driver, which was not needed in the Morse Code device driver, was the installation of an interrupt handler. The Morse Code driver simply took advantage of the services of the existing interrupt handler for the timer interrupt.

# 11.4.1 Setting Up a New Interrupt Handler

Most device drivers need an ISR to handle interrupts which come from the device. The Linux function `request_irq()` takes care of the installation of a new handler. Its definition is located in /usr/src/linux/arch/i386/kernel/irq.c.

```
int request_irq(unsigned int irq,
```

# Table 11.1. ASCII Code Chart

0 Ctrl-@ 32 <SPC> 64 @ 96 ' 1 Ctrl-A 33 ! 65 A 97 a 2 Ctrl-B 34 " 66 B 98 b 3 Ctrl-C 35 # 67 C 99 c 4 Ctrl-D 36 $ 68 D 100 d 5 Ctrl-E 37 % 69 E 101 e 6 Ctrl-F 38 & 70 F 102 f 7 Ctrl-G 39 ' 71 G 103 g 8 Ctrl-H 40 ( 72 H 104 h 9 Ctrl-I 41 ) 73 I 105 i 10 Ctrl-J 42 * 74 J 106 J 11 Ctrl-K 43 + 75 K 107 k 12 Ctrl-L 44 , 76 L 108 l 13 Ctrl-M 45 - 77 M 109 m 14 Ctrl-N 46 . 78 N 110 n 15 Ctrl-O 47 \ 79 O 111 o 16 Ctrl-P 48 0 80 P 112 p