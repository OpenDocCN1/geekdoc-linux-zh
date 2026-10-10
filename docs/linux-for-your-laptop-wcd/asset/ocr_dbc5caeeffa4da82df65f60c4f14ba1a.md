# iBook Trade-Off

You can use the iBook's internal modem if you use the Yaboot Boot utility and boot Yellow Dog Linux using Apple's Open Firmware prompt. However, your X11 sessions will be limited to 256 colors. If you boot Yellow Dog Linux using the BootX control panel, the internal modem will not work, but you'll be able to use X with thousands of colors!

The good news is that at least one project is attempting to develop an Open Source driver for some of these devices. Browse to
http://www.linmodems.org

You can read a alternative view about how to use these chips with Linux, such as for an answering machine, call recording, and so on. You'll find the source code for this ongoing project, along with a (predictable) binary-only driver from Lucent in the form of a 500Kb+ kernel module. The driver, named lucent.o, has been reported to work with a number of Lucent chipsets in different notebooks. While this book was written, I tested an IBM ThinkPad 390X, Mandrake 7.0, and the lucent.o module, and found that reliable connections were possible at speeds up 38400Kbps.

The other good news is that not all notebook manufacturers use these devices. Some notebooks on the market include "real" internal modems! Although the manufacturer rarely touts this as a marketing point, such laptops (like the Sony 505TX and TR) are highly prized items with mobile Linux users.

Notebooks may also be ordered without an internal modem. If so, buy a supported PCMCIA 56K V.90 modem or a combination Ethernet/modem card. Some of the best modem cards are those that do not rely on proprietary cables (or dongles) but instead have a pop-out tab sporting an RJ-11 telephone jack. If you are looking for an excellent combination card that does not use proprietary dongles or take up two Type II slots, the Linksys EtherFast 10/100 + 56K V.90 PCMCIA card is an excellent choice. This card features built-in RJ-11 and RJ-45 ports for telecommunications and network. You'll also be able to use another Type II card if you have two PCMCIA slots in your notebook.

When you've determined what serial port is used by your internal modem (hint: use dmesg to look for /dev/ttyS1 output), you should use the ln command to create a symbolic link named /dev/modem for use by communications programs or when connecting to the Internet:

```
$ ln -s /dev/ttyS1 /dev/modem
```