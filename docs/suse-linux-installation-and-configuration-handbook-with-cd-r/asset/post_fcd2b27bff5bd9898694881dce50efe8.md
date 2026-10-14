
cards, whereas external modems are devices that reside outside the machine, such as a printer or scanner. External modems connect to the serial port through a serial cable. All external modems work on Linux whether they are PnP or non-PnP.

## What Are Win-Modems?

Win-modems are not modems in the sense that they do not have some chips that were originally found on normal modems; instead, win-modems use software capabilities to implement the functions of those chips. One advantage of this technique is the fact that win-modems are easy to upgrade because they're software-oriented. However, one disadvantage is that replacing hardware functions with software puts more overhead on your processor.

## Does Linux Support Win-Modems?

Up to the writing of this book, we had heard of only two win-modems that are supported (Alpha Stage). This means that Linux can run those modems. The only problem facing programmers is that the manufacturers would not release the source of their drivers for those modems, nor would they release a comprehensive design sheet. Therefore, if you asked any Linux user, he'd tell you to avoid win-modems. For more information on the level win-modem support has reached, check the following site: http://www.linmodems.org.

## Does Linux Support PCI Modems?

The 2.2.x series of the Linux kernel does not support serial ports on PCI devices at the time of this writing. In other words, the 2.2.x series does not support PCI modems. However, the 2.3.x series partially supports serial interfaces on PCI devices. This means that the next stable 2.4.x series will have good support of PCI modems. Although, we might get some support for the PCI serial port in 2.2.x after this book has been published. In general, stick to the external and ISA modems for the time being.

## Plug-and-Play Modems

Linux does not support PnP devices by itself; rather it does so through a special package called isapnptools. The only problem with PnP devices in general is that you have to go through the process of setting up everything that has to do with the device. The program isapnp is very comprehensive and easy to use, so you should not have any trouble setting up all the PnP devices on your system.

## How Modems Communicate with the Computer

Modems communicate with the computer through the serial port. Internal modems have a built-in serial port, whereas external modems use an existing serial port on your machine through a serial cable. Still, like any normal device on the system, modems have I/O ports and IRQs. You should not confuse the serial port with the I/O port—these are two different things.

TIP To communicate with the computer, modems require a serial port, an I/O port, and an IRQ.

## Serial Ports and Linux

As a POSIX-compatible OS, all the devices in Linux are found in the /dev directory. Thus, you will find all the serial ports in this directory. Linux maps the serial ports starting from ttyS0. Table 23.1 shows the mapping of the serial ports when using DOS/Win9x/WinNT and Linux.

Table 23.1 DOS/Win9x/WinNT and Linux Ports Mapping

| DOS/Win | Linux |
|---|---|
| com 1 | /dev/ttyS0 |
| com 2 | /dev/ttyS1 |
| com 3 | /dev/ttyS2 |
| com 4 | /dev/ttyS3 |

As mentioned in the previous section, internal modems have a built-in serial port. This built-in serial port can be changed either through jumper/DIP switch setting in the case of a traditional card or through software in the case of a PnP card. External modems will use an existing serial port just as mice do.

## Setting Up a New Modem

The process of setting up a new modem involves the following steps:

- 1. Setting up software requirements
- 2. Configuring the modem
- 3. Configuring the serial port
- 4. Telling YaST where the modem is
- 5. Testing and troubleshooting

## Modem Connection Software Requirements

Package requirements:
Series a:

- modules
- net_tool
- netcfg
- kernmod (only if you don't want to recompile your kernel)
- isapnp (for PnP modems)
- pciutils (for automatic configuration of PnP cards)
- nkita (Packages nkita and nkitb have security holes in all SuSE versions up to 6.2. You might want to upgrade them from the SuSE FTP site. The new secure version is available on the accompanying CD.)
- nkitb

Series n:

- ppp
- wvdial (only for SuSE 6.1 and earlier; 6.2 users use YaST)
- minicom
- inetcfg

Kernel requirements:

- Character devices, standard/generic (dumb) serial support
- Network device support, dummy net driver support
- Network device support, PPP if you use a PPP connection
- Network device support, SLIP if you use a SLIP connection

You can have those kernel requirements installed as built in or as modules if you don't know the type of your ISP connection. For SLIP type connections, you can include the CSLIP for SLIP compression. Another option for slow SLIP connections is the Keep Alive and Linefill. This option ensures that your connection is not accidentally terminated.

## Configuring the Modem

Setting up the modem is an easy task, yet you have to consider which type of modem you're currently using. Internal and external modems are generally set up using one of the following methods:

- Traditional jumper/DIP switch setting
- PnP setup

## Setting Up the Modem

At this point, you want to direct the modem to use the available resources on your computer. You want the modem to pick up a free serial port, IRQ, and correct port. Here you'll learn about the two types of internal modems—the traditional jumper/DIP switch setting and the PnP modems.

To find out where the available resources are on the machine, you have to use the proc filesystem that holds all of your computer's information.

To pick a free IRQ, do the following:

```
bash#cat /proc/interrupts
```

The previous command will list the used IRQs on your system, so you can pick up a free one.

The following example illustrates how to find an unused IRQ:

```
bash#cat /proc/interrupts
CPU0
0:       167388          XT-PIC  timer
1:         5185          XT-PIC  keyboard
2:            0          XT-PIC  cascade
5:            0          XT-PIC  soundblaster
6:            2          XT-PIC  rtc
11:       12237          XT-PIC  eth0
13:            1          XT-PIC  fpu
14:      335341          XT-PIC  ide0
15:            6          XT-PIC  ide1
```

In this example, notice that interrupt 4 is free. Tell the serial port to use this free interrupt.

> **NOTE** Note that the PCI system allows interrupt sharing; for example, two serial ports can use the same IRQ but with different I/O ports. This means that even if IRQ 4 is already taken by another serial port, it is still possible to share it with the modem serial port.

> **CAUTION**
> The following IRQs should not be used because they belong to motherboard resources. If you use any of them you will either slow down the performance of your Linux box or lock it up. Those interrupts are 1, 2, 6, 8, 9, 13, and 14.

## Setting Up the Modem's Jumper/DIP Switch Settings

In some cases, this process might require that you have the modem's manual. If you have an internal modem, then you will need to change the placement of some jumpers/DIP switches. If you have an external modem, it's more likely that the changes will be made through buttons or DIP switches. You will have to change the serial port to a suitable and free one through the jumpers/DIP switches. Also, in most cases, you will have the ability to change the IRQ and I/O port.

## Setting Up a PnP Modem

This is a simple process once you know what you're doing. First, you have to know that Linux by itself does not support PnP auto device configuration. You have to do this manually, which means that you won't get the full advantage of PnP devices. You will get only the ability to control the PnP device via software. This might be a curse instead of a blessing. PnP devices do not save the settings that you make to them. So, when you shut down your system and start it again, the settings might change. This was causing Linux users problems until a very important package was implemented: isapnp tools.
