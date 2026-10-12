
## TIP

Linux is not as verbose in its description of hardware components. However, you can still resolve the hardware types under Linux later by consulting the `/proc/` directory. Here there are several files that dynamically list CPU information, interrupts, and I/O ports.

Likewise, you can identify some of the more elusive interrupt requests (IRQs) and port settings in the same manner. At the same screen, make sure that the Computer element at the top of the dialog box is highlighted, then click on the Properties button below. The screen shown in Figure 1.2 should appear. Here you can identify the IRQ setting for each card.

However, the newer release of Red Hat Linux already probes many of the ports, video, network, and sound cards. Often, Linux does a better job at identifying all the components than does Windows 95/98 or 2000. If the Linux kernel doesn't automatically recognize a device, several tools exist (such as `sndconfig` and `kudzu`), which will accomplish additional probing for devices and let you force IRQ and port settings if you know them. Again, the `/proc/` directory lists the different interrupts and ports that Linux uses for each component.

Using the command `cat /proc/interrupts` will show you what interrupts are being used by which devices. The same directory, i.e. `/proc/`, includes several other dynamic files that will provide information on the CPU, ports, and memory usage.

![](img/a0884097af3186d9b4f616aaa3f065b0_49_0.png)

### FIGURE 1.2

Become familiar with the various IRQs and port settings required by each component before attempting to make them all talk under Linux.

While configuring an older machine for one of our employees, I had partitioned half of a 9 gigabyte SCSI hard drive for Windows 98 while reserving the other half for Linux. The machine had over 196 megabytes of RAM and several peripheral devices, including an obscure SCSI card. It also had an older network card and an internal tape drive. Windows failed to detect the network card or the tape drive. It did load a generic driver for the SCSI card so that I could at least install the operating system. Full configuration of the machine required several hours of painstaking work. After downloading updated drivers for the network card, I was finally able to make it function, but I gave up on the tape drive. I was less than optimistic as I began installing Linux. I had recently purchased a cheap copy of Red Hat 6.0 and decided to install it on the other 4.5 gigabytes of available hard drive space. Linux detected the network card without a hitch and then proceeded to inform me that it had also detected a tape backup device. I had Linux completely installed and operational in under an hour.

Granted, not all machines are configured or made equally. To quote George Orwell in *Animal Farm*, “…some are more equal than others.” Your experience may not be as positive as mine, but as Linux matures and as manufacturers make the hardware specifications more accessible, detection of parts and cards will become even easier.

### Knowing Your Hardware

Before doing any sort of install on your machine, be sure you are familiar with the computer parts and components. Knowing the history of the hardware also doesn’t hurt. In my case, I knew I had an older SMC network card on my own computer, but I had to discover on my own that it required the older Western Digital drivers. Before undertaking any sort of install on Linux, you should be sure of two things: first, know exactly what cards, chipsets and components make up your computer, and second, be sure that what you have is compatible with the Linux release you will be using.

If you have any question as to whether your parts will work with Red Hat, first check the Red Hat site and follow the link to the Hardware Compatibility List. The rule of thumb is that if the part is not listed, it is not supported. You may have to look closely to verify that your parts are or are not listed. (I’ve had to find out the hard way that many of the older Intel NIC cards that I thought were listed were in fact not supported by even the latest version of Linux. Instead Linux supported the newer cards.) The Hardware Compatibility List is divided into different sections according to type. It is simple to verify that even the most antiquated sound card is well supported by the latest Red Hat.

It requires only a quick perusal to find several mirrored pages that list the core components currently supported by Linux. The *Linux Compatibility HOWTO* is probably the most comprehensive. This list goes through all the parts that do and could possibly be integrated into a desktop computer running Linux. The items supported are listed in the following order:

- motherboards/BIOS
- laptops
- CPU
- memory
- video cards
- controllers (ranging from hard drives to RAID to SCSI to multiports)
- network adapters
- sound cards
- hard drives
- tape drives
- CD-ROMs
- CD writers
- removable drives
- mice
- modems
- printers
- scanners
- and every other possible peripheral imaginable, from joysticks to amateur radios

Because many of the drivers for certain components do overlap, simply knowing what type of chipset your parts use is also quite helpful. This is true in the case of video and Ethernet cards. A particular brand may not be listed by name, but its chip should certainly appear in the list, if supported.

It used to be that only a limited number of parts and accessories worked under Linux, but today nearly any off-the-shelf item will either function under the average Linux install or can be made to function with a bit of effort. If you have components that you are unsure about and the main Red Hat site is unclear as to their compatibility, a quick posting to a newsgroup or consultation with your friendly neighborhood computer guru can quickly dispel any doubts. And if all else fails, there is probably a better or newer part, also likely to be cheaper, available at the nearest computer shop. Also, manufacturers have begun releasing specifications for more and more parts and making more drivers available. Hardware packaging with the term “Works with Linux” has become commonplace. Though you may feel comfortable that your hardware will work, it never hurts to double-check the compatibility lists to verify that your item is listed. If you are still unable to find out, contact the manufacturer. Many companies today make information about their products available on the Internet. Usually a quick visit to their home page will dispel any uncertainty.

## CONFIGURING AND INSTALLING RED HAT LINUX

Chapter 1

### TIP

Some of the best places to look for information are on the Linux distributors page and the Linux Documentation Project (LDP) home page. The latter is probably the better choice since it is maintained by an army of volunteers dedicated to publishing information and specifications on all brands of Linux hardware and software and everything else in between. If you can’t find an answer there, then someone still needs to write it. The site’s current URL is `http://www.linuxdoc.org`.

Originally based in North Carolina, the LDP is mirrored on geographically diverse sites and has contributors from all over the globe. The LDP not only provides documentation and helpful HOWTOs, but also hosts a wide array of resources including source code for a vast assemblage of Linux programs and links to resources and guides, documentation, mailing lists, news, and online journals all dedicated to keeping the Linux user up-to-date.

Before taking any steps to install, it helps to write down all the specifications, the card types (including the manufacturer and model number), and any other printed information located on the device. It is far easier to consult your own notes than to attempt to consult the hardware after it is installed and the machine is running. This is especially true for hard drives located in inconvenient places. There have been a couple occasions when I have had to remove a part to verify its product number or chipset.

### TIP

You should make a detailed list of every separate component. You can then refer to the list when installing.

### Preparing for the Install

With most Linux distributions and with the newer motherboards, nearly all machines can boot up the Linux installation directly off the CD-ROM. You will first need to consult your motherboard’s BIOS to make sure this option is available. Check the option marked “Boot Sequence” or something similar, usually located under the *BIOS Features Setup*, to see whether your machine can initially boot off the CD-ROM. If so, change the configuration to make the CD-ROM the boot drive; then insert the Linux CD and power up the machine. The installation routine should start automatically after verifying the BIOS settings.
