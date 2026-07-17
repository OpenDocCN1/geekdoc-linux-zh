![](Images/cover00315.jpeg)

Linux and Raspberry Pi

Basic Projects for Beginners, Kids, Makers & Professionals

Hacks, Python & IoT Projects Included

Tech Knowledge Democratization

STEAM Education

By Mario Meraz

To my daughter since I do a lot of things in inspiration from her to be a better father and to democratize the knowledge.

To my mother because She was always asking me when do you launch a new book?. Thanks, Mother, for Educate me.

![A picture containing text Description automatically generated](Images/image00264.jpeg)

Table of Contents

[About the Author](#part0000.xhtml__Toc119614492)

[Preface](#part0000.xhtml__Toc119614493)

[Introduction](#part0000.xhtml__Toc119614494)

[Conventions used in this book](#part0000.xhtml__Toc119614495)

[Raspberry Pi Models & History](#part0000.xhtml__Toc119614496)

[The Starter Kit](#part0000.xhtml__Toc119614497)

[Linux Systems and Architectures](#part0001.xhtml__Toc119614498)

[File Systems](#part0001.xhtml__Toc119614499)

[Getting the Pi Up and Running](#part0001.xhtml__Toc119614500)

[Special Settings](#part0001.xhtml__Toc119614501)

[Linux Commands for Raspberry Pi](#part0001.xhtml__Toc119614502)

[General Purpose Input Output (GPIO)](#part0002.xhtml__Toc119614503)

[Python the Basics](#part0002.xhtml__Toc119614504)

[All about Raspberry pi Projects](#part0002.xhtml__Toc119614505)

[What is the internet of Things (IoT) ?](#part0002.xhtml__Toc119614506)

[Project with python and OLED Display](#part0002.xhtml__Toc119614507)

[Project Python Script, The famous “Hello World!” plus your name](#part0002.xhtml__Toc119614508)

[Project Monitoring your CPU](#part0002.xhtml__Toc119614509)

[Project Temperature Sensor](#part0002.xhtml__Toc119614510)

[Project BMP180 Sensor (Pressure, Temperature and Altitude) .](#part0002.xhtml__Toc119614511)

[Projects with the Raspberry Pi Camera](#part0002.xhtml__Toc119614512)

[Fundamental Projects to build your Stack of Knowledge.](#part0002.xhtml__Toc119614513)

[Project Twilio: Send an SMS from the Raspberry Pi](#part0002.xhtml__Toc119614514)

# About the Author

![A picture containing text, person, person, indoor Description automatically generated](Images/image00265.jpeg)

Mario Meraz

He is a professional who currently works for Cisco Systems in Dallas, Texas, United States of America, participating in high technology projects around the technologies of 5G, Cybersecurity, Internet of Things (IoT), Network Function Virtualization(NFV), DevOps, OpenRAN, Software Define Networks(SDN), Data Centers, Cloud, Smart Cities, Blockchain, Packet Core, SaaS (Software as Services), among other technologies.

Mario Meraz has worked directly or as a Consultant, Business Development Manager, Architect, Software Engineer and Product Manager through one of his direct employers or accounts during his career for global companies such as: Verizon Wireless (USA), AT&T (USA, Mexico), T-Mobile (USA), Ericsson (USA), Nokia Siemens Network ( USA), América Móvil (Global), Century Link (Global), Rogers Canada, Google (Global), Facebook (Global), Amazon (Global), Microsoft (Global) among other companies and service providers.

Mario Meraz has a PhD in Development Economics, a Master in Big Data and Data Science, a Master in Software Development, a Master in Business Administration and a Bachelor in Electronic Engineering. Mario, due to his personal and professional career, considers himself a Humanitarian and Technologist “Dactivist”, likewise he has created a space on YouTube, to open a dialogue with access to all audiences on current technological issues, the name of this channel on YouTube is called: OpenDemocraTech Space.

Disclaimer: The content of this book expresses the sole opinion of the author and does not reflect in any way the opinion of current or past, nor future employers, clients, accounts, and partners.

Mario Meraz can be reached through the following means:

Twitter: @merazmario

[http://linkedin.com/in/mario-meraz-9200305b](http://linkedin.com/in/mario-meraz-9200305b)

www.mariomerazauthor.com

Copyright  @2022 by Mario Meraz . United States of America

U.S. Copyright Act of 1976.

Disclaimer

The content in this book is for educational purposes only. The software, code and scripts in this book are provided “as is” without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose and noninfringement. In no event shall the author of this book (Mario Meraz) is liable for any claim, damages or other liability, whether in an action of contract, tort or otherwise, arising from, out of or in connection with the software or use or other dealings in the software, code and scripts here presented in the book the github links and the web site: [www.mariomerazauthor.com](http://www.mariomerazauthor.com)

# Preface

This book is all about educational purposes, this book is an attempt to democratize the tech knowledge. This book entails practical Linux Operating Systems knowledge, raspberry pi concepts ,tech-hacks and practical Internet of Things (IoT) projects with sensors, OLED displays and python scripts, even third-party solutions to send SMS like Twilio through Application Programming Interfaces (APIs).

You maybe have seen the cover of this book and have thought for yourself , yet another book of raspberry pi , well yes, but not, and let me explain what is the intention of this book, basically this book has three objectives : learn Linux, start learning a raspberry-pi fundamentals and the third aspect is to be useful as a reference material around Linux Operating Systems , that’s the reason why I listed the whole output for some cli commands in order to provide a reference, another big aspect of this book is that I don’t make assumptions that everyone should know how to get from step A to step Z. I listed all the steps in order to level up the knowledge for the new linux, raspberry makers and enthusiasts or even professionals interested in brushing up your knowledge.

Raspberry Pi is all about education. These devices have shown the value through numerous examples around education and learning of computing science concepts, Linux Systems, makers projects and even gaming and entertainment. The Raspberry Pi is one of the most exciting things to happen in combination and at the same time to the computer, electronics worlds and education field in recent years that have expanded the possibilities of creative maker projects but also real applications an industrial use cases.

One personal motivation to put together this book is the fact that I consider a raspberry-pi a democratizer of the technical knowledge and I myself claim to be a democratizer of the technical knowledge, I really believe that the starting point for a technical career could be the technical knowledge learnt through a raspberry-pi projects.

As an education tool, this tiny PC has reignited interest in bare-metal computing in schools, factories, homes and even some enterprises all over the world. As a platform for open-source software, it has also inspired millions of people to try Linux, many for the fists time. Most exciting of all is the potential to incorporate the device into practical projects, as demonstrated by this book.

# Introduction

The microcontroller market is a 28 billion-unit per year business. Since this is a book about raspberry pi, it is mandatory to speak about Eben Upton the CEO and Founder of the Raspberry Pi Foundation.

Nine years ago, the Raspberry was born, since then the Raspberry Pi Foundation has sold 42 million devices. The evolution has been big from Raspberry Pi 1 to the Raspberry Pi 2 from one single core to a quad core configuration. Although the biggest jump has been from 3+ to 4  (C).

In 2021 the Raspberry Foundation has started to produce the RP2040 chip which has been introduced in the microcontroller dev board Pi Pico Raspberry.

Benefits of a Raspberry 

Silent, low power, small machines, used for Edge and IoT Computing, Community device oriented.

Raspberry uses the ARM Processor and there are a lot of ARM small devices around like mobile devices with this type of processor. There are big models of Raspberry Pi, also there are small models like the Raspberry Pi Zero and the raspberry pi pico. In this book we will discuss and focus on the Raspberry Pi 4.

Prerequisites

Some of the prerequisites of this book are the ones below, although these are not mandatory since I tried to write this book from zero to hero approach.

*   Just a little of Networking

*   Just a little of Linux, although no worries here you will learn the foundation of Linux with the Raspbian OS which is a variant of Debian.

*   And last but not least a lot of interest in learning and having fun!

# Conventions used in this book

Constant with bold: Used for folders, filenames, and file extensions and CLI (Command Line Interface) instructions.

Italic: Indicates URLs, New Terms and text that should be typed literally by the user.

![Icon Description automatically generated](Images/image00266.jpeg)  

This icon above is to point out an important note

![Icon Description automatically generated](Images/image00267.jpeg)

This icon above indicates warning and caution

![A picture containing icon Description automatically generated](Images/image00268.jpeg)

This icon above indicates a Hack a Technical Hint that could be in the cybersecurity realm

![Icon Description automatically generated](Images/image00269.jpeg)

This icon above indicates that there are python scripts or python knowledge to encompassed

# Raspberry Pi Models & History

Raspberry Chronology and History.

To know the past and the evolution of this amazing device lets go to a little review of the raspberry history and evolution to these days.

| Year | 2012 | 2013 | 2014 | 2015 |
| Model | Model B | Model A | Model B+ | Model Zero |
| Feature | Genesis Design | Simpler and Cheaper | Improved layout | Smaller and cheaper |

| Year | 2015 | 2016 | 2017 | 2018 |
| Model | Model 3B  | Model 3B | Model Zero Wireless | Model 3A+/B+ |
| Feature | More RAM (From to 2GB) | Faster, Wifi, BT | Wifi, Bluetooth  | Faster, USB Boot |

Raspbian OS Version History

| Raspbian Operating System Version History |
| 2012 | 2015 | 2017 | 2019 |
| Wheezy | Jessie | Stretch | Buster |
|  |  |  |  |

Raspberry Pi 4 Model B

A super charged Raspberry Pi that finally does everything you would want it to, for the exact same price as the previous models.

While the raspberry Pi has enjoyed years of success, there’s always been a couple of things a lot of users wanted. A slightly more powerful CPU that could handle day-to-day computing, plenty of USB ports and maybe wireless to make connecting the network easier. The Pi 4 Model B  comes with two micro-HDMI ports, this HDMI ports are capable of outputting 4K video, two USDB 3.0 and two USB 2.0 ports, one USB-C power input, one Ethernet port for wired internet, one headphone jack (3.5mm) for sound, and a 40-pin GPIO port.

![A picture containing electronics Description automatically generated](Images/image00270.jpeg)

Pi 4 Model B files are compatible with files produced in previous Raspberry pi models.

In this book we will work with a Raspberry Pi 4, although any model can be utilized

Raspberry 4

64 Bit CPU 

Faster (1.5 GHz)

More RAM (From 1,2, to 4 GB)

Gigabit Ethernet Ports

2.4 GHz and 5 GHz WiFi

Bluetooth 5.0 / BLE

USB 3.0 Port

Dual, 4K HDMI Output

BCM2711 Chip

The BCM2711 chip of the Raspberry Pi 4 Model B is a quad-core 1.5 GHz processor.

GPIO Port

![Icon Description automatically generated](Images/image00266.jpeg)

40 pins in the GPIO Port. Lay out per Pinout

![Table Description automatically generated](Images/image00271.jpeg)

![Graphical user interface, application Description automatically generated](Images/image00272.jpeg)

Image taken from [https://www.raspberrypi-spy.co.uk/2012/06/simple-guide-to-the-rpi-gpio-header-and-pins/](https://www.raspberrypi-spy.co.uk/2012/06/simple-guide-to-the-rpi-gpio-header-and-pins/)

Ethernet Port

The Gigabit Ethernet for wired networks on the Pi 4 and Pi 3 Model B+ are three times faster than older Pi models.

USB Ports

Two USDB 3.0 and two USB 2.0 ports, one USB-C power input

Integrated Wireless

The Pi 4 Model B has Wireless Capabilities for Wi-Fi and Bluetooth

802.11n wireless LAN

Bluetooth 5.0

Micro SD Port

For the Operating System Cards

Micro-HDMI Ports

The Raspberry Pi 4 Model B decode 4K video.

Since the Raspberry Pi 4 Model B has two Micro-HDMI ports These ports can be used for dual-display support.

Headphone Jack

3.5 mm jack

# The Starter Kit

Below are the pictures of the starter kit needed to start off learning the nuts and bolts of the Raspberry Pi.

![A picture containing text, electronics Description automatically generated](Images/image00273.jpeg)

Keyboard, Mouse. Power Cable and Mini-HDMI Cable

![Graphical user interface Description automatically generated](Images/image00274.jpeg)

SD Card (minimum 64 GB) for the Operating System Image

The Operating System can be chosen from the page below:

https://www.raspberrypi.com/software/operating-systems/

![Graphical user interface, text, application, email Description automatically generated](Images/image00275.jpeg)

The Raspberry Pi Imager can be downloaded in the link below:

[Https://www.raspberrypi.org/software/](Https://www.raspberrypi.org/software/)

![Graphical user interface, application Description automatically generated](Images/image00276.jpeg)

The CLI instruction to install the image is the one below:

mariomeraz@raspberrypi:~ $ sudo apt install rpi-imager

To flash the Operating System for the Raspberry pi BalenaEtcher can be downloaded in the link https://www.balena.io/etcher/

![A screenshot of a computer Description automatically generated with medium confidence](Images/image00277.jpeg)

![A picture containing electronics, circuit Description automatically generated](Images/image00278.jpeg)

![A close-up of a computer chip Description automatically generated with medium confidence](Images/image00279.jpeg)

![A picture containing text, indoor, electronics, set Description automatically generated](Images/image00280.jpeg)

Cases, there are a lot of options

Additional Accessories

![Graphical user interface Description automatically generated](Images/image00281.jpeg)  ![Graphical user interface, text Description automatically generated with medium confidence](Images/image00282.jpeg)

Powered USB hub

![Graphical user interface, application Description automatically generated](Images/image00283.jpeg)  ![Text Description automatically generated with medium confidence](Images/image00284.jpeg)

SD Card Readers either USB C or USB 3.0

# Linux Systems and Architectures

Linux systems have evolved tremendously over the last few years. Learning and mastering how the Linux operating systems could lead to anyone to job placements, promotions and merit pay increases. The Linux Architecture and logic is helpful not only to understand Linux systems, but also Cloud Architectures such as google cloud logic.

This command “lscpu” is the utility to know the Architecture of the system. Along “lscpu”  fetches the CPU architecture information from the “sysfs” .

mariomeraz@raspberrypi:~ $ lscpu

Architecture:                    armv7l

Byte Order:                      Little Endian

CPU(s):                          4

On-line CPU(s) list:             0-3

Thread(s) per core:              1

Core(s) per socket:              4

Socket(s):                       1

Vendor ID:                       ARM

Model:                           3

Model name:                      Cortex-A72

Stepping:                        r0p3

CPU max MHz:                     1800.0000

CPU min MHz:                     600.0000

BogoMIPS:                        108.00

Vulnerability Itlb multihit:     Not affected

Vulnerability L1tf:              Not affected

Vulnerability Mds:               Not affected

Vulnerability Meltdown:          Not affected

Vulnerability Spec store bypass: Not affected

Vulnerability Spectre v1:        Mitigation; __user pointer sanitization

Vulnerability Spectre v2:        Vulnerable

Vulnerability Srbds:             Not affected

Vulnerability Tsx async abort:   Not affected

Flags:                           half thumb fastmult vfp edsp neon vfpv3 tls vfp

                                 v4 idiva idivt vfpd32 lpae evtstrm crc32

mariomeraz@raspberrypi:~ $ 

Some of the commands expressed here are listed in the LPI Certification (Linux Professional Institute) which is a non-profit group that provides exams and qualifications around Linux Systems and Architectures.

Even though the material in this book don’t fully prepare you to take The LPI Certification, the logic and approach of the knowledge presented follows the levels of the LPI Certification around General System Administration, Hardware Configuration, Package Management , Command Line and Processes Handling. If you have been using and playing with Linux for a while, perhaps you might be somewhat familiar, although it’s worth going through anyway in the potential case there is snippet of knowledge that you are missing.

Some of the command line outputs in these books are useful for Rad Hat Enterprise Linux (RHEL) distros and CentOS, Debian alike versions. Open Systems based on Linux Architecture provides information about devices and peripherals.

Virtual Directories created by the Kernel contain information about running process and hardware devices such as “/proc” which is focused on supplying information about processes such as read which are programs running on the system. And “/sys” covers hardware devices.

Note: There is a saying in Linux and Unix alike systems that if there is no news is because it is good news.

mariomeraz@raspberrypi:~ $ cd /proc

mariomeraz@raspberrypi:/proc $ ls

1     1734  2038  234  391  561  71   85         cpuinfo        misc

10    1736  205   237  392  574  72   853        crypto         modules

100   1737  2055  238  393  582  732  87         devices        mounts

1086  1739  2057  239  394  6    74   88         device-tree    net

1087  1762  2058  240  399  605  75   883        diskstats      pagetypeinfo

1092  1763  2059  241  4    606  754  887        driver         partitions

11    1765  206   25   40   61   757  892        execdomains    schedstat

1159  1783  2061  252  400  62   76   896        fb             self

12    18    2065  26   404  625  77   9          filesystems    slabinfo

120   1807  207   27   405  63   773  90         fs             softirqs

1222  1857  208   3    406  630  776  903        interrupts     stat

1242  1906  209   30   408  631  78   907        iomem          swaps

13    193   2095  31   41   645  786  913        ioports        sys

132   1941  21    32   410  646  789  92         irq            sysrq-trigger

1378  195   2114  33   411  647  791  93         kallsyms       sysvipc

1390  1952  2120  37   414  65   792  94         keys           thread-self

14    1964  2128  38   415  658  8    95         key-users      timer_list

15    198   2135  380  434  659  80   99         kmsg           tty

16    2     2140  382  466  66   801  asound     kpagecgroup    uptime

163   20    2156  383  481  667  81   buddyinfo  kpagecount     version

1653  200   2157  384  484  67   811  bus        kpageflags     vmallocinfo

17    2027  2158  385  492  68   82   cgroups    latency_stats  vmstat

1709  2028  22    386  493  7    828  cmdline    loadavg        zoneinfo

1710  2029  223   39   494  70   83   consoles   locks

1730  2034  228   390  557  705  84   cpu        meminfo

mariomeraz@raspberrypi:/proc $

mariomeraz@raspberrypi:/ $ cd /sys

mariomeraz@raspberrypi:/sys $ ls

block bus class  dev  devices  firmware  fs  kernel  module  power

Some of the internal devices in any computer sit on a data transfer system called the PCI Bus.

In some old systems the information can be visualized with the following cli command

mariomeraz@raspberrypi:$ cat /proc/pci

In newer distros the information can be displayed as follows:

mariomeraz@raspberrypi:/ $ cd /sys/bus

mariomeraz@raspberrypi:/sys/bus $ ls

amba         cpu           i2c              mmc          platform  usb

cec          event_source  iscsi_flashnode  mmc_rpmb     scsi      workqueue

clockevents  genpd         mdio_bus         nvmem        sdio

clocksource  gpio          media            pci          serial

container    hid           mipi-dsi         pci_express  spi

mariomeraz@raspberrypi:/sys/bus $

But the data is not readable, reason why the suitable cli command to read the device data is with the following cli command:

mariomeraz@raspberrypi:$ /sbin/lspci

mariomeraz@raspberrypi:/dev

![Icon Description automatically generated](Images/image00266.jpeg)

                   I will start with this main concept that the core philosophy of Unix and Linux Systems is that everything and when I say everything is a FILE. Especially your hardware besides the documents and images.

The /dev directory contains hardware device nodes, which are files representing devices.

mariomeraz@raspberrypi:/sys $ cd /dev

mariomeraz@raspberrypi:/dev $ ls

autofs         loop4         ram8            tty26  tty57      vcsa6

block          loop5         ram9            tty27  tty58      vcsa7

btrfs-control  loop6         random          tty28  tty59      vcsm-cma

bus            loop7         rfkill          tty29  tty6       vcsu

cachefiles     loop-control  rpivid-h264mem  tty3   tty60      vcsu1

cec0           mapper        rpivid-hevcmem  tty30  tty61      vcsu2

cec1           media0        rpivid-intcmem  tty31  tty62      vcsu3

char           media1        rpivid-vp9mem   tty32  tty63      vcsu4

console        media2        serial1         tty33  tty7       vcsu5

cuse           mem           shm             tty34  tty8       vcsu6

disk           mmcblk0       snd             tty35  tty9       vcsu7

dma_heap       mmcblk0p1     stderr          tty36  ttyAMA0    vga_arbiter

dri            mmcblk0p2     stdin           tty37  ttyprintk  vhci

fb0            mqueue        stdout          tty38  uhid       video10

fd             net           tty             tty39  uinput     video11

full           null          tty0            tty4   urandom    video12

fuse           port          tty1            tty40  v4l        video13

gpiochip0      ppp           tty10           tty41  vchiq      video14

gpiochip1      ptmx          tty11           tty42  vcio       video15

gpiomem        pts           tty12           tty43  vc-mem     video16

hidraw0        ram0          tty13           tty44  vcs        video18

hidraw1        ram1          tty14           tty45  vcs1       video20

hidraw2        ram10         tty15           tty46  vcs2       video21

hwrng          ram11         tty16           tty47  vcs3       video22

i2c-20         ram12         tty17           tty48  vcs4       video23

i2c-21         ram13         tty18           tty49  vcs5       video31

initctl        ram14         tty19           tty5   vcs6       watchdog

input          ram15         tty2            tty50  vcs7       watchdog0

kmsg           ram2          tty20           tty51  vcsa       zero

log            ram3          tty21           tty52  vcsa1

loop0          ram4          tty22           tty53  vcsa2

loop1          ram5          tty23           tty54  vcsa3

loop2          ram6          tty24           tty55  vcsa4

loop3          ram7          tty25           tty56  vcsa5

mariomeraz@raspberrypi:/dev $

The Device nodes are created automatically by the kernel, some of the devices are placed in subdirectories such as the following.

mariomeraz@raspberrypi:$ snd (sound cards/ chips)

mariomeraz@raspberrypi:/dev $ ls snd

by-path    controlC1  pcmC0D0p  pcmC2D0p  timer

controlC0  controlC2  pcmC1D0p  seq

mariomeraz@raspberrypi:/dev $

mariomeraz@raspberrypi:$ input (mouse)

mariomeraz@raspberrypi:/dev $ ls input

by-id  by-path  event0  event1  event2  event3  event4  event5  mice  mouse0

mariomeraz@raspberrypi:/dev $

The following direction is used to redirect output of a command, so it doesn’t show on the screen, literally “/dev/null “ eats data and destroys it.

mariomeraz@raspberrypi:/dev $ ls null

null

mariomeraz@raspberrypi:/dev $

The “/dev/mem holds the machine’s RAM

mariomeraz@raspberrypi:/dev $ ls mem

mem

mariomeraz@raspberrypi:/dev $

With the string and pipeline and pipeline we can see what text the RAM chips are currently holding.

Driver Modules

In case there is a need to disable a device. The hardware driver enables the device at the same time the driver can be enabled at the time of Kernel compilation.

The modules can be found as follows:

/lib/modules/<kernel version>/kernel.

Indeed, the Kernel has the capability to load modules when it detects certain pieces of hardware. In order to list the modules that the Kernel has currently loaded the following command can be used as root:

mariomeraz@raspberrypi:~ $ lsmod

Module                  Size  Used by

rfcomm                 49152  4

cmac                   16384  3

algif_hash             16384  1

aes_arm_bs             24576  2

crypto_simd            16384  1 aes_arm_bs

cryptd                 24576  2 crypto_simd

algif_skcipher         16384  1

af_alg                 28672  6 algif_hash,algif_skcipher

bnep                   20480  2

hci_uart               40960  1

btbcm                  16384  1 hci_uart

bluetooth             405504  31 hci_uart,bnep,btbcm,rfcomm

ecdh_generic           16384  2 bluetooth

ecc                    40960  1 ecdh_generic

8021q                  32768  0

garp                   16384  1 8021q

stp                    16384  1 garp

llc                    16384  2 garp,stp

uinput                 20480  1

snd_soc_hdmi_codec     20480  2

brcmfmac              335872  0

brcmutil               20480  1 brcmfmac

cfg80211              765952  1 brcmfmac

rfkill                 32768  6 bluetooth,cfg80211

vc4                   278528  17

cec                    49152  1 vc4

raspberrypi_hwmon      16384  0

v3d                    77824  15

drm_kms_helper        274432  3 vc4

gpu_sched              45056  1 v3d

snd_soc_core          233472  2 vc4,snd_soc_hdmi_codec

snd_compress           20480  1 snd_soc_core

snd_pcm_dmaengine      16384  1 snd_soc_core

snd_bcm2835            24576  1

snd_pcm               114688  6 snd_compress,snd_pcm_dmaengine,snd_soc_hdmi_codec,snd_bcm2835,snd_soc_core

bcm2835_codec          45056  0

bcm2835_v4l2           45056  0

bcm2835_isp            32768  0

v4l2_mem2mem           36864  1 bcm2835_codec

bcm2835_mmal_vchiq     32768  3 bcm2835_isp,bcm2835_codec,bcm2835_v4l2

videobuf2_vmalloc      16384  1 bcm2835_v4l2

videobuf2_dma_contig    20480  2 bcm2835_isp,bcm2835_codec

i2c_brcmstb            16384  0

videobuf2_memops       16384  2 videobuf2_dma_contig,videobuf2_vmalloc

videobuf2_v4l2         32768  4 bcm2835_isp,bcm2835_codec,bcm2835_v4l2,v4l2_mem2mem

snd_timer              32768  2 snd_pcm

videobuf2_common       65536  8 bcm2835_isp,bcm2835_codec,videobuf2_dma_contig,videobuf2_vmalloc,videobuf2_memops,bcm2835_v4l2,v4l2_mem2mem,videobuf2_v4l2

snd                    81920  16 snd_compress,snd_soc_hdmi_codec,snd_timer,snd_bcm2835,snd_soc_core,snd_pcm

vc_sm_cma              32768  2 bcm2835_isp,bcm2835_mmal_vchiq

syscopyarea            16384  1 drm_kms_helper

sysfillrect            16384  1 drm_kms_helper

videodev              245760  6 bcm2835_isp,bcm2835_codec,videobuf2_common,bcm2835_v4l2,v4l2_mem2mem,videobuf2_v4l2

mc                     49152  6 bcm2835_isp,bcm2835_codec,videobuf2_common,videodev,v4l2_mem2mem,videobuf2_v4l2

sysimgblt              16384  1 drm_kms_helper

fb_sys_fops            16384  1 drm_kms_helper

rpivid_mem             16384  0

nvmem_rmem             16384  0

uio_pdrv_genirq        16384  0

uio                    20480  1 uio_pdrv_genirq

i2c_dev                20480  0

drm                   536576  16 v3d,vc4,gpu_sched,drm_kms_helper

drm_panel_orientation_quirks    16384  1 drm

backlight              20480  2 drm_kms_helper,drm

fuse                  131072  3

ip_tables              28672  0

x_tables               32768  1 ip_tables

ipv6                  520192  60

mariomeraz@raspberrypi:~ $

Note: In some distros to list the same output it’s needed the prefix /sbin

mariomeraz@raspberrypi:~ $ /sbin/ lsmod

mariomeraz@raspberrypi:/sbin $ lsmod

Module                  Size  Used by

rfcomm                 49152  4

cmac                   16384  3

algif_hash             16384  1

aes_arm_bs             24576  2

crypto_simd            16384  1 aes_arm_bs

cryptd                 24576  2 crypto_simd

algif_skcipher         16384  1

af_alg                 28672  6 algif_hash,algif_skcipher

bnep                   20480  2

hci_uart               40960  1

btbcm                  16384  1 hci_uart

bluetooth             405504  31 hci_uart,bnep,btbcm,rfcomm

ecdh_generic           16384  2 bluetooth

ecc                    40960  1 ecdh_generic

8021q                  32768  0

garp                   16384  1 8021q

stp                    16384  1 garp

llc                    16384  2 garp,stp

uinput                 20480  1

snd_soc_hdmi_codec     20480  2

brcmfmac              335872  0

brcmutil               20480  1 brcmfmac

cfg80211              765952  1 brcmfmac

rfkill                 32768  6 bluetooth,cfg80211

vc4                   278528  17

cec                    49152  1 vc4

raspberrypi_hwmon      16384  0

v3d                    77824  15

drm_kms_helper        274432  3 vc4

gpu_sched              45056  1 v3d

snd_soc_core          233472  2 vc4,snd_soc_hdmi_codec

snd_compress           20480  1 snd_soc_core

snd_pcm_dmaengine      16384  1 snd_soc_core

snd_bcm2835            24576  1

snd_pcm               114688  6 snd_compress,snd_pcm_dmaengine,snd_soc_hdmi_codec,snd_bcm2835,snd_soc_core

bcm2835_codec          45056  0

bcm2835_v4l2           45056  0

bcm2835_isp            32768  0

v4l2_mem2mem           36864  1 bcm2835_codec

bcm2835_mmal_vchiq     32768  3 bcm2835_isp,bcm2835_codec,bcm2835_v4l2

videobuf2_vmalloc      16384  1 bcm2835_v4l2

videobuf2_dma_contig    20480  2 bcm2835_isp,bcm2835_codec

i2c_brcmstb            16384  0

videobuf2_memops       16384  2 videobuf2_dma_contig,videobuf2_vmalloc

videobuf2_v4l2         32768  4 bcm2835_isp,bcm2835_codec,bcm2835_v4l2,v4l2_mem2mem

snd_timer              32768  2 snd_pcm

videobuf2_common       65536  8 bcm2835_isp,bcm2835_codec,videobuf2_dma_contig,videobuf2_vmalloc,videobuf2_memops,bcm2835_v4l2,v4l2_mem2mem,videobuf2_v4l2

snd                    81920  16 snd_compress,snd_soc_hdmi_codec,snd_timer,snd_bcm2835,snd_soc_core,snd_pcm

vc_sm_cma              32768  2 bcm2835_isp,bcm2835_mmal_vchiq

syscopyarea            16384  1 drm_kms_helper

sysfillrect            16384  1 drm_kms_helper

videodev              245760  6 bcm2835_isp,bcm2835_codec,videobuf2_common,bcm2835_v4l2,v4l2_mem2mem,videobuf2_v4l2

mc                     49152  6 bcm2835_isp,bcm2835_codec,videobuf2_common,videodev,v4l2_mem2mem,videobuf2_v4l2

sysimgblt              16384  1 drm_kms_helper

fb_sys_fops            16384  1 drm_kms_helper

rpivid_mem             16384  0

nvmem_rmem             16384  0

uio_pdrv_genirq        16384  0

uio                    20480  1 uio_pdrv_genirq

i2c_dev                20480  0

drm                   536576  16 v3d,vc4,gpu_sched,drm_kms_helper

drm_panel_orientation_quirks    16384  1 drm

backlight              20480  2 drm_kms_helper,drm

fuse                  131072  3

ip_tables              28672  0

x_tables               32768  1 ip_tables

ipv6                  520192  60

mariomeraz@raspberrypi:/sbin $

To obtain further information about the functionality of the modules the following option can be used:

mariomeraz@raspberrypi:$ /sbin/modinfo dm_mod

mariomeraz@raspberrypi:/sbin $ ls modinfo

mariomeraz@raspberrypi:/sbin $

mariomeraz@raspberrypi:~ $ cat /proc/cpuinfo

processor : 0

model name : ARMv7 Processor rev 4 (v7l)

BogoMIPS : 76.80

Features : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32 

CPU implementer : 0x41

CPU architecture: 7

CPU variant : 0x0

CPU part : 0xd03

CPU revision : 4

processor : 1

model name : ARMv7 Processor rev 4 (v7l)

BogoMIPS : 76.80

Features : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32 

CPU implementer : 0x41

CPU architecture: 7

CPU variant : 0x0

CPU part : 0xd03

CPU revision : 4

processor : 2

model name : ARMv7 Processor rev 4 (v7l)

BogoMIPS : 76.80

Features : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32 

CPU implementer : 0x41

CPU architecture: 7

CPU variant : 0x0

CPU part : 0xd03

CPU revision : 4

processor : 3

model name : ARMv7 Processor rev 4 (v7l)

BogoMIPS : 76.80

Features : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32 

CPU implementer : 0x41

CPU architecture: 7

CPU variant : 0x0

CPU part : 0xd03

CPU revision : 4

Hardware : BCM2835

Revision : a02082

Serial : 000000007b72c055

Model : Raspberry Pi 3 Model B Rev 1.2

mariomeraz@raspberrypi:~ $

mariomeraz@raspberrypi:~ $ lsusb

Bus 001 Device 005: ID 04d9:1702 Holtek Semiconductor, Inc. Keyboard LKS02

Bus 001 Device 004: ID 046d:c05a Logitech, Inc. M90/M100 Optical Mouse

Bus 001 Device 003: ID 0424:ec00 Standard Microsystems Corp. SMSC9512/9514 Fast Ethernet Adapter

Bus 001 Device 002: ID 0424:9514 Standard Microsystems Corp. SMC9514 Hub

Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

mariomeraz@raspberrypi:~ $ 

mariomeraz@raspberrypi:~ $ lsblk

NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT

mmcblk0     179:0    0 59.5G  0 disk 

\u251c\u2500mmcblk0p1 179:1    0  256M  0 part /boot

\u2514\u2500mmcblk0p2 179:2    0 59.2G  0 part /

mariomeraz@raspberrypi:~ $

Hardware-less booting

There is an option to install Linux without peripherals which is through network booting.  This method is called PXE (Pre-boot Execution Environment). This functionality is a sort of firmware on some CPU processes that scan the network for an NBP (Network Bootstrap Program). Although for the PXE to work, it will need the DCHP and TFTP servers enabled on the network along with the appropriate boot files.

Udev

Udev is a background process that creates device nodes and interfaces with hardware in the /dev location. The programs interact with the Udev via D-Bus, which is an inter-process communication system (IPC) which enable programs to send messages among themself. One example of this is in the desktop environment which can request status to the D-Bus to know if any new device has been plugged in, therefore the D-Bus collects this status information from the “Udev” when the user plugs in any hardware, therefore inform the process in the desktop to display a dialog box or launch an application.

Ethernet Connection

Raspberry Pi Models with Ethernet port. The Raspberry Pi can communicate via SSH with an Ethernet cable. There is a package that includes the zero-conf software with a daemon available called “avahi-daemon”

mariomeraz@raspberrypi:/ $ sudo apt install avahi-daemon

Reading package lists... Done

Building dependency tree... Done

Reading state information... Done

avahi-daemon is already the newest version (0.8-5).

The following package was automatically installed and is no longer required:

  libfuse2

Use 'sudo apt autoremove' to remove it.

0 upgraded, 0 newly installed, 0 to remove and 70 not upgraded.

mariomeraz@raspberrypi:/ $

Keyboard Hint

![A picture containing icon Description automatically generated](Images/image00268.jpeg)  If for any reason the keyboard layout needs to be customized, the following sequence of commands will be useful.

Keyboard Configuration

mariomeraz@raspberrypi:/ $ sudo dpkg-reconfigure keyboard-configuration

The following screen will pop-up

![Graphical user interface, text, application Description automatically generated](Images/image00285.jpeg)

Daemon

When a service request comes in normally a daemon is tarted automatically running continuously the Linux internet services. The /etc/services file lists network services and the commonly used subnet of services. The IANA (Internet Assigned Numbers Authority) maintains a database of all registered services.

[https://www.iana.org/](https://www.iana.org/)

![Graphical user interface Description automatically generated with medium confidence](Images/image00286.jpeg)

In terms of the executable files, most of the daemons are stored in /usr/sbin. The naming convention specifies that the names for many of them should end with the letter (d) to distinguish them from utilities. In order to look for the daemon programs on the local system it is needed to search at /usr/sbin/ *d

![A picture containing icon Description automatically generated](Images/image00268.jpeg) A Daemon is a Service Process which runs in the background and these Daemon services supervises the Linux system which provides functionalities to the process in the system. Since the Daemons run in the background by hackers these services are preferred to be explored by Hackers, and you know what?  MIT (Massachusetts Institute of Technology) Hackers were the ones who coined the “Daemon” name.

Some of the Daemons can be found inside the run folder.

mariomeraz@raspberrypi:/run $ ls -ll

total 24

drwx------  3 root              root     60 Jun  7 22:09 alsa

drwxr-xr-x  2 avahi             avahi    80 Jun  7 22:09 avahi-daemon

drwxr-xr-x  2 root              root     80 Jun  7 22:09 blkid

drwxr-xr-x  2 root              root     80 Jun  7 22:09 console-setup

drwxr-xr-x  2 root              root     40 Mar 27 00:42 credentials

-rw-r--r--  1 root              root      4 Jun  7 22:09 crond.pid

----------  1 root              root      0 Jun  7 22:09 crond.reboot

drwxr-xr-x  3 root              lp      100 Jun  7 22:09 cups

drwxr-xr-x  2 root              root     60 Jun  7 22:09 dbus

-rw-r--r--  1 root              root      4 Jun  7 22:09 dhcpcd.pid

srw-rw----  1 root              root      0 Jun  7 22:09 dhcpcd.sock

srw-rw-rw-  1 root              root      0 Jun  7 22:09 dhcpcd.unpriv.sock

drwxr-xr-x  2 root              root     60 Jun  7 22:09 dnsmasq

prw-------  1 root              root      0 Mar 27 00:42 initctl

drwx--x--x  3 root              root     60 Jun  7 22:09 lightdm

-rw-r--r--  1 root              root      4 Jun  7 22:09 lightdm.pid

drwxrwxrwt  3 root              root     80 Jun  7 22:09 lock

drwxr-xr-x  3 root              root     60 Jun  7 22:09 log

-rw-r--r--  1 root              root     77 Jun  7 22:09 motd.dynamic

drwxr-xr-x  2 root              root     40 Mar 27 00:42 mount

drwxr-xr-x  2 root              root    100 Jun  7 22:09 network

drwxr-xr-x  2 root              root     40 Jun  7 22:09 plymouth

drwxr-xr-x  4 root              root     80 Jun  7 22:36 resolvconf

-rw-r--r--  1 root              root      4 Jun  7 22:09 rngd.pid

drwxr-xr-x  2 _rpc              root     40 Jun  7 22:09 rpcbind

dr-xr-xr-x 11 root              root      0 Mar 27 00:42 rpc_pipefs

drwxr-xr-x  2 root              root     40 Jun  7 22:09 sendsigs.omit.d

lrwxrwxrwx  1 root              root      8 Jun  7 22:09 shm -> /dev/shm

drwxr-x---  3 speech-dispatcher audio   100 Jun  7 22:09 speech-dispatcher

drwx--x--x  3 root              root     60 Jun  7 22:09 sudo

drwxr-xr-x  2 root              root     60 Jun  7 22:09 sysconfig

drwxr-xr-x 20 root              root    480 Jun  7 22:09 systemd

srw-rw-rw-  1 root              root      0 Jun  7 22:09 thd.socket

drwxr-xr-x  2 root              root     60 Mar 27 00:42 tmpfiles.d

drwxr-xr-x  7 root              root    160 Jun  7 22:09 udev

drwx------  2 root              root     40 Jun  7 22:09 udisks2

drwxr-xr-x  3 root              root     60 Jun  7 22:09 user

-rw-rw-r--  1 root              utmp   1536 Jun  7 22:09 utmp

drwxr-x---  2 root              netdev   80 Jun  7 22:09 wpa_supplicant

mariomeraz@raspberrypi:/run $

For more services look at this link https://datatracker.ietf.org/doc/html/rfc1700

| Daemon | Used for or by | Function |
| acpid | Advanced Configuration and power interface | Flexible daemon for delivering ACPI events. Replaces apmd daemon. |
| apmd | Advanced Power Management | Reports and acts on specified changes in system power, including shutdowns. Useful with machines, such as laptops, that run on batteries |
| atd | at | Executes a command once at a specific time and date. See crond for period execution of a command |
| automount | Automatic Mounting | Automatically mounts filesystems when they are accessed. Auto-matic mounting is a way of demand-mounting remote directories without having to hard-configure them into /etc/fstab |
| crond | cron | Used for period execution of tasks. This daemon looks in the /var/spool/cron directory for files with filenames that correspond to user’s usernames. It also looks at the /etc/crontab file and at files in the /etc/cron.d directory.When a task comes up for execution, crond executes it as the user who owns the file that describes the task. |
| dhcpcd | DHCP | DHCP Client daemon |
| dhcpd | DHCP | Assigns Internet Address, subnet mask, default gateway, DNS, and other information to hosts. This protocol answers DHCP requests and, optionally , BOOTP requests. |
| ftpd | FTP | Handles FTP requests |
| gpm | General Purpose mouse or GNU paste manager | Allows you to use a mouse to cut and paste text on console applications |
| httpd | HTTP | The web server daemon |
| In.fingerd | finger | Handles requests for user information from the finger utility launched by xinetd |
| inetd |  | Deprecated in favor of xinetd |
| lpd | Line printer spooler Daemon | Launched by xinetd when printing requests come to the machine. Not used with CUPs |
| named | DNS | Supports DNS |
| Nfsd, statd, lockd, mountd, rquotad | NFS | These five daemons operate together to handle NFS operations.The nfsd daemon handles file and directory requests.The statd and locd daemons implement network file and record locking. The mountd daemon converts filesystem name requests from the mount utility into NFS handles and checks access permissions. If disk quotas are enabled, rquotad handles those. |
| ntpd | NTP | Synchtonizes time on network computers. Ntpd requires a /etc/ntp.conf file. (www.ntp.org) |
| portmap | RPC | Maps incoming requests for RPC service numbers to TCP or UDP port numbers on the local system. |
| pppd | PPP | This protocol controls the pseudo interface represented by the IP connection between the local computer and a remote computer. |
| rexecd | rexec | Allows a remote user with a valid username and password to run programs on a system. Its use is generally deprecated for security reasons. |
| routed | Routing Tables | Manages the routing tables so the system knows where to send messages that are destined for remote networks. If the system doesn’t have an etc/defaultrouter file, routed is started automatically to listen to incoming routing messages and to advertise outgoing routes to other systems on the local network. |
| rsyslogd | System Log | Transcribes important system events and stores them in files and forwards them to users or another host running the rsyslogd daemon. This daemon is configured with /etc/rsyslog.conf and used with the rsyslog utility. |
| sendmail | Mail Programs | The sendmail daemon came from Berkeley UNIX and has been available for a long time. The sendmail daemon always listens on port 25 for incoming mail connections and then calls a local delivery agent, such as /bin/mail. |
| Smbd, nmbd | Samba | Allow Windows PCs to share files and printers with Linux operating systems computers. |
| sshd | Ssh, scp | Enables secure logins between remote systems. |
| talkd | talk | Allows the user to have a conversation with another user on the same or remote machine. The talkd daemon handles the connections between machines. |
| telnetd | TELNET | One of the original Internet remote access protocols |
| tftpd | TFTP | Used to boot a system or get information from a network. |
| timed | Time Series | On a LAN synchronizes time with other computers that are also running timed daemon. |
| xinetd | Internet Superserver | This daemon listens for service requests on the network  connections and starts up the appropriate daemon to respond to any request. |

# File Systems

A File System in Linux is a structured collection of files on a disk drive or a disk array and a partition, where a partition is a segment of memory. The Linux Filesystem holds directories of files. The Linux Filesystem’s structure store systems data and user data on a storage device.

The Hierarchical approach 

The Linux File System uses a hierarchical structure to organize and store data. The topmost directory in the Linux structure is de / directory also known as the root directory. This hierarchy structure is important because it provides the Filesystem Hierarchy Standard (FHS) which  ensures consistency among systems and also different Linux distributions. 

The FH Standard provides the structure: 

*   For ensuring the data is organized
*   To make sure the integrity of the stored data
*   The Data can be easily located and retrieved

“ls” List contents of the current directory

mariomeraz@raspberrypi:~$ ls /

mariomeraz@raspberrypi:/ $ ls

bin   dev  home  lost+found  mnt  proc  run   srv  tmp  var

boot  etc  lib   media       opt  root  sbin  sys  usr

mariomeraz@raspberrypi:~$

mariomeraz@raspberrypi:$ which ls

| Directory | Description |
| /root | Root Directory |
| /bin | In this directory there are programs, files and commands that all users can run |
| /boot | Here there are all the files needed at boot time |
| /dev | At this location there are special files that represent the devices on the user’s system |
| /etc | At this directory the configuration files can be found |
| /etc/init.d | Scripts to start-up services |
| /etc/X11 | X1 Configuration files |
| /home | User home directory |
| /home/pi | Home Directory for the “Pi” user |
| /lib | Kernel Modules and Drivers |
| /media | Mount points for removable media |
| /proc | This is a virtual directory with information about running processes and the Operating System |
| /sbin | Programs for System Maintenance |
| /sys | This a special directory on the Raspberry Pi that represents the hardware devices |
| /tmp | Space for programs to create temporary files |
| /usr | At this directory there are programs and data usable by all users |
| /usr/bin | Most of the programs in the operating system that the user interacts reside here |
| /usr/games | Here is where the games reside |
| /usr/lib | In this location there are libraries to support common programs |
| /usr/local | All the software that are specific to this machine go here |
| /usr/sbin | System Administration Programs |
| /usr/share | Objects that are shared between applications like icons of fonts for instance |
| /usr/src | The source of the Linux distro goes here, since Linux is open source |
| /var | This is the location where the system logs and spool files can be found |
| /var/backups | In this directory there are backup copies of most of the system files |
| /var/cache | In this location there are any programs that cache data , for example apt-get or web browsing |
| /var/log | Location for all the system logs and individual service logs |
| /var/mail | All user email is stored at this location if mail has been configured |
| /var/spool | At this location there are Data waiting to be processed. |

# Getting the Pi Up and Running

Raspberry Pi Configuration Options (raspi-config)

In the Graphical Configuration Interface (GUI) there are a couple of options that can be selected with the up and down arrows to move around the list.

The following steps will walk you through the steps on the configuration options.

Click on the Raspberry Symbol -> ![](Images/image00287.jpeg) Then Go to Preferences -> Then Go to Raspberry Pi Configuration and you will see the screen below

On the setting option tools, use the Up and Down arrows to move around the list of options. To select the “options” the space bar needs to be used.

![Graphical user interface Description automatically generated](Images/image00288.jpeg)

![Graphical user interface, text, application Description automatically generated](Images/image00289.jpeg)

![Graphical user interface, table Description automatically generated](Images/image00290.jpeg)

![Graphical user interface Description automatically generated](Images/image00291.jpeg)

![Graphical user interface Description automatically generated](Images/image00292.jpeg)

Expand rootfs

This option will enlarge the file system to use the whole SD capacity.

Overscan

This option is useful to fit the image in the screen. Initially this option is disabled. For the high-definition monitors sometimes the texts run off the side of the screen, in order to fix this issue, it is needed to enable the overscan to change the values to fit the image to the screen. The values in the overscan option indicate the amount of overscan on the images, therefore, to correct any issue with the images, the positive values could go off the screen and the negative values can be used to to correct the black borders around the edge of the display.

Keyboard

There is an option to select the keyboard type.

Password

Initially the default password is raspberry, although in the latest version there is an option to set-up the initial password at the time of first set-up.

Change Locale

The default settings are for UK English with a standard UTF-8-character encoding.

Change Time Zone

This option can be used to change the time depending on the location and time zone

SSH

This option turns on the Secure Shell (SSH) server, to log-in to the raspberry pi remotely over a network.

Memory Split

The default value is split. This option allows to change the amount of memory used by the CPU and the GPU.

Overclock

This provides the option of running the processor at speeds higher than 700 MHz.

Other options are Medium or Modest and Turbo mode that can run at 1000 MHz.

Below is the sequence to perform this action through cli commands” Boost performance and Overclocking”

mariomeraz@raspberrypi:$ sudo raspi-config

Options:

Modest

Medium

High

Turbo

mariomeraz@raspberrypi:$ sudo shutdown -r now

# Special Settings

Overclock

The overclock function provides a 50 percent extra of performance at not extra cost. The processor in the raspberry pi is designed to run at 700 MHz, which means that performs 700,000,000 operations per second. Although doing over clocking increases the power consumption which by consequence increases the amount of heat generated.

To activate the overlocking function as follows:

mariomeraz@raspberrypi:~ $ sudo raspi-config

Select “overclocking”

Notes: The maximum overlocking setting will increase an extra 50% speed.

Raspberry pi will automatically turn off overcooking once it reaches 85 Celsius degrees

Since overlocking will increase the amount of power that the raspberry pi draws, the raspberry pi will become less stable at the time of running several USB devices at the same time.

# Linux Commands for Raspberry Pi

Desktop Behavior

This option is used to boot straight to the graphical desktop environment which is set to “Yes” by default. If the option “No” is selected the command line will be displayed when the process of boot up is completed, and it will be required to log-in to start the graphical interface.

The below credentials are the default credentials:

Raspberrypi login: pi

Password: raspberry

To start the raspy-config GUI (Graphic User Interface)

mariomeraz@raspberrypi:~ $ startx

Update.

This option is to update the Operating System. The CLI alternative to do this is the following:

mariomeraz@raspberrypi:~ $ sudo reboot

$ = Regular User command

# = root user command

{The latter must be used as root or by using the Sudo command}

How to add users

#adduser <username>

#passwd <username>

Use the cli commands below update and Upgrade the Raspberry Pi Operating System

mariomeraz@raspberrypi:# apt -get # This cli can be used to install and remove software.

mariomeraz@raspberrypi:# sudo apt-get install <program> # This cli command will install the <program> package.

mariomeraz@raspberrypi:# sudo apt-get update  # This cli will grab an up-to-date list of packages from the repository.

mariomeraz@raspberrypi:# sudo reboot {Reboot the Raspberry Pi}

mariomeraz@raspberrypi:# sudo shutdown -h now {Shutdown the Raspberry Pi }

mariomeraz@raspberrypi:# sudo apt-get upgrade     # This cli command will upgrade all packages that have a newer version in the repository.

mariomeraz@raspberrypi:# sudo apt-get purge <program> # This cli command will remove the <program> package.

mariomeraz@raspberrypi:~ $ sudo apt-get purge

Reading package lists... Done

Building dependency tree... Done

Reading state information... Done

The following package was automatically installed and is no longer required:

  libfuse2

Use 'sudo apt autoremove' to remove it.

0 upgraded, 0 newly installed, 0 to remove and 217 not upgraded.

mariomeraz@raspberrypi:~ $ 

mariomeraz@raspberrypi:# apt-cache search <program>  # This will search the repository for all packages relating to keywords.

Navigation and Files

The Commands below are utilities and instructions that are essential to work with Linux systems, remember in Linux everything is a file. Linux is all about files.

![Icon Description automatically generated](Images/image00266.jpeg)

Important to know; to terminate or interrupt the output of a cli instruction press Control – C or Control -Z  then these instructions will interrupt the output of any instruction in Linux and other programs like python.

| CLI Command | Action |
| Man <cli command> | Provides extensive definition of all the cli commands with functions and options |
| pwd | Show the current working directory |
| mkdir | Make a directory |
| Ls | List contents of the current directory |
| Cd | Change directory |
| Mv | Move or rename a file or directory |
| Cp | Copy file or files |
| Rm | Remove file or riles |
| rmdir | Remove directory |

mariomeraz@raspberrypi:~ $  cd {Change directory}

mariomeraz@raspberrypi:~ $  cd ~ {moves to the home directory}

mariomeraz@raspberrypi:~ $  cd / {moves to the root directory}

mariomeraz@raspberrypi:~ $  cd .. {moves back one directory}

Example:
mariomeraz@raspberrypi:~ $ cd /home/pi/Documents

mariomeraz@raspberrypi:~ $ cd ./Music

mariomeraz@raspberrypi:~ $ cd ..

mariomeraz@raspberrypi:~ $  cd ~

Finding Files

Find <location> <test>

Useful flags include: -mtime <number> find files modified in the last <number> of days.

For instance, <number> could be, for example, 2 (exactly two days ago), -2 (less than two days ago), +2 (more than two days ago)

-name <filename> find files called <filename> -iname <filename> matches file called <filename>but not case-sensitive.

Wildcards

(*) Matches any string of characters, or no characters

(?) Matches any singe character

[abc] Matches a,b,c

[!abc] Matches any character except a, b, c

[A-Z] Matches any character in the range A-Z

[one, two] Matches the words one and two

Special Keys

Ctrl + C Kills whatever program is running in the terminal

Ctrl + D Sends the end-of-file character to whatever program is running in the terminal

Ctrl +Shift + C Copies selected text to the clipboard

Ctrl +Shift + V Pastes text from the clipboard

Create new user account

mariomeraz@raspberrypi:$ sudo adduser name

mariomeraz@raspberrypi:$ sudo adduser name sudo

“uname” Displays system information

mariomeraz@raspberrypi:~ $ uname

Linux

mariomeraz@raspberrypi:~ $ 

“pwd” Displays the current directory

mariomeraz@raspberrypi:~ $ pwd

/home/mariomeraz

mariomeraz@raspberrypi:~ $

The “ls” command list all the files

mariomeraz@raspberrypi:~ $ ls

list files

The option “a” list the invisible files

mariomeraz@raspberrypi:~ $ ls -a

list all files (including hidden ones)

mariomeraz@raspberrypi:~ $ ls -la

total 108

drwxr-xr-x 15 mariomeraz mariomeraz  4096 Nov  1 20:15 .

drwxr-xr-x  3 root       root        4096 May 19 18:47 ..

-rw-------  1 mariomeraz mariomeraz  1171 Nov  1 20:15 .bash_history

-rw-r--r--  1 mariomeraz mariomeraz   220 Apr  4  2022 .bash_logout

-rw-r--r--  1 mariomeraz mariomeraz  3523 Apr  4  2022 .bashrc

drwxr-xr-x  2 mariomeraz mariomeraz  4096 Apr  4  2022 Bookshelf

drwxr-xr-x  7 mariomeraz mariomeraz  4096 Jun  7 22:09 .cache

drwx------ 13 mariomeraz mariomeraz  4096 Jun  7 22:28 .config

drwxr-xr-x  2 mariomeraz mariomeraz  4096 May 19 18:47 Desktop

drwxr-xr-x  2 mariomeraz mariomeraz  4096 Jun  7 22:52 Documents

drwxr-xr-x  2 mariomeraz mariomeraz  4096 Jun  7 21:33 Downloads

-rw-r--r--  1 mariomeraz mariomeraz 15359 Nov  1 19:56 index.html

-rw-r--r--  1 mariomeraz mariomeraz   367 Nov  1 20:14 index.html.1

drwxr-xr-x  3 mariomeraz mariomeraz  4096 Apr  4  2022 .local

drwxr-xr-x  2 mariomeraz mariomeraz  4096 May 19 18:47 Music

drwxr-xr-x  2 mariomeraz mariomeraz  4096 May 19 18:47 Pictures

drwx------  3 mariomeraz mariomeraz  4096 May 19 18:48 .pki

-rw-r--r--  1 mariomeraz mariomeraz   807 Apr  4  2022 .profile

drwxr-xr-x  2 mariomeraz mariomeraz  4096 May 19 18:47 Public

drwxr-xr-x  2 mariomeraz mariomeraz  4096 May 19 18:47 Templates

drwxr-xr-x  2 mariomeraz mariomeraz  4096 May 19 18:47 Videos

-rw-------  1 mariomeraz mariomeraz    56 Nov  1 20:15 .Xauthority

-rw-------  1 mariomeraz mariomeraz  2976 Nov  1 20:15 .xsession-errors

-rw-------  1 mariomeraz mariomeraz  2976 Nov  1 20:00 .xsession-errors.old

mariomeraz@raspberrypi:~ $ 

mariomeraz@raspberrypi:~ $ ls -l

lists more information about each file.

The option mkdir is useful to create a new directory

mariomeraz@raspberrypi:$ mkdir newdirectory

In order to create an empty file, the touch file can be used

mariomeraz@raspberrypi:$ touch empty

To rename the file the mv option can be used

mariomeraz@raspberrypi:$ mv empty newname

To remove the file

mariomeraz@raspberrypi:$ rm newname

To remove an empty directory, use rmdir

mariomeraz@raspberrypi:$ rmdir emptydirectory

To remove a directory that has files in it use the option -r (This r comes from recursive, which indicates the rm option should recursively delete everything in the directory.

mariomeraz@raspberrypi:$ directory > rm -r

Installing Software

mariomeraz@raspberrypi:$ tar zxvf fiel.tar.gz

mariomeraz@raspberrypi:$ tar xjf file.tar.bz

mariomeraz@raspberrypi:$./configure

Whenever a program’s route code is unzipped

After zipped a Program “cd” into that directory and “run ./configure”. This will verify that the system has everything it needs to compile the software. The cli command make will compile the software if is needed.

mariomeraz@raspberrypi:$  (sudo) make install  # This cli will move the newly compiled software into the appropriate place in the system so the user can run it like a normal cli command.

Commands to write Data to RAM

fstab for fast performance Configuration

mariomeraz@raspberrypi:$ sudo nano /etc/fstab

Addition of the following lines are to mount a virtual file system:

tmpfs /var/log tmpfs defaults,noatime,nosuid,mode=0755,size=100m 0 0

mariomeraz@raspberrypi:$ sudo shutdown -r now

After the restarting process, the virtual file system will be mounted on var/log on the RAM disk. There are other directories that can be moved to RAM as well  and need to be added through nano in /etc/fstab as follows:

Tmpfs /tmp tmpfs defaults,noatime,nosuid,size=100m 0 0

Tmpfs /var/tmp tmpfs defaults,noatime,nosuid,size=30m 0 0

Tmpfs /var/log tmpfs defaults,noatime,nosuid,mode=0755, size=100m 0 0

Tmpfs /var/run tmpfs defaults,noatime,nosuid,mode=0755, size=2m 0 0

Tmpfs /var/spool/mqueue tmpfs defaults,noatime,nosuid,mode=0700, size=100m gid=12, size=30m 0 0

Commands to manage disk partitions

mariomeraz@raspberrypi:$ sudo apt-get install gdisk

mariomeraz@raspberrypi:$ sudo disk /dev/sdb

mariomeraz@raspberrypi:~ $ sudo apt update

Get:1 https://download.docker.com/linux/raspbian buster InRelease [33.6 kB]

Get:2 http://archive.raspberrypi.org/debian buster InRelease [32.6 kB]         

Get:3 http://raspbian.raspberrypi.org/raspbian buster InRelease [15.0 kB]      

Get:4 https://download.docker.com/linux/raspbian buster/stable armhf Packages [21.1 kB]

Get:5 http://raspbian.raspberrypi.org/raspbian buster/main armhf Packages [13.0 MB]

Get:6 http://archive.raspberrypi.org/debian buster/main armhf Packages [392 kB]

Get:7 http://raspbian.raspberrypi.org/raspbian buster/contrib armhf Packages [58.8 kB]

Get:8 http://raspbian.raspberrypi.org/raspbian buster/non-free armhf Packages [104 kB]

Fetched 13.7 MB in 49s (281 kB/s)                                              

Reading package lists... Done

Building dependency tree       

Reading state information... Done

224 packages can be upgraded. Run 'apt list --upgradable' to see them.

N: Repository 'http://raspbian.raspberrypi.org/raspbian buster InRelease' changed its 'Suite' value from 'stable' to 'oldstable'

N: Repository 'http://archive.raspberrypi.org/debian buster InRelease' changed its 'Suite' value from 'testing' to 'oldstable'

mariomeraz@raspberrypi:~ $

Df -h

Displays the amount of space left on the device.

mariomeraz@raspberrypi:~ $ df -h

Filesystem      Size  Used Avail Use% Mounted on

/dev/root        59G  3.9G   53G   7% /

devtmpfs        3.7G     0  3.7G   0% /dev

tmpfs           3.9G   22M  3.9G   1% /dev/shm

tmpfs           1.6G  1.3M  1.6G   1% /run

tmpfs           5.0M  4.0K  5.0M   1% /run/lock

/dev/mmcblk0p1  253M   50M  203M  20% /boot

tmpfs           790M   44K  790M   1% /run/user/1000

mariomeraz@raspberrypi:~ $ 

![A picture containing icon Description automatically generated](Images/image00268.jpeg)“wget” This utility is a Hack. “wget” is the non-interactive network downloader wget is a free utility for non-interactive download of files from the Web server even when the user has not logged on to the system and it can work in the background without hindering the current process. This GNU utility supports HTTP, HTTPS, and FTP protocols, as well as retrieval through HTTP proxies.

In this example below the google domain is taken as an example.

mariomeraz@raspberrypi:~ $ wget www.google.com

--2022-11-07 13:46:09--  http://www.google.com/

Resolving www.google.com (www.google.com)... 2607:f8b0:4023:1006::93, 2607:f8b0:4023:1006::68, 2607:f8b0:4023:1006::67, ...

Connecting to www.google.com (www.google.com)|2607:f8b0:4023:1006::93|:80... connected.

HTTP request sent, awaiting response... 200 OK

Length: unspecified [text/html]

Saving to: ‘index.html.2’

index.html.2            [ <=>                ]  14.70K  --.-KB/s    in 0.01s   

2022-11-07 13:46:09 (1.36 MB/s) - ‘index.html.2’ saved [15053]

mariomeraz@raspberrypi:~ $ 

USB (Universal Serial Bus)

When the USB device is plugged in any Linux system the kernel initially probes it to find out what class it belongs to. USB devices are organized into classes to facilitate driver development. There are classes for all sorts of devices such as audio, webcams, printers, keyboards, mouse, joysticks and even for vendor specific classes. USB devices attached on the Raspberry Pi and How to mount and USB device as a hard drive on the Raspberry Pi.

List of all attached USB devices (ls + usb)

mariomeraz@raspberrypi:~ $  lsusb

To reduce the among of output data of the “lsusb” cli command it could be utilized the verbose option as follows:

mariomeraz@raspberrypi:~ $  lsusb -v

The following command shows the devices in a tree-like format to see the dices connected:

mariomeraz@raspberrypi:~ $ lsusb -t

To see further information about the USB controllers and the devices connected such as directories for each device with the files containing: manufacturer name, speed, maximum power usage and more information.

mariomeraz@raspberrypi:~ $ /sys/ bus/ usb/devices

Mount point creation

mariomeraz@raspberrypi:~ $  sudo mkdir /media/usb

Pi User as the folder owner

mariomeraz@raspberrypi:~ $ sudo chown -R pi:pi /media/usb

Mounting the USB drive

mariomeraz@raspberrypi:~ $  sudo mount /dev/sda1 /media/ usb -o uid=pi,gid=pi

The cli command to find out information about the USB controller are the following.

To find the UUID (Universal Unique Identifier)

mariomeraz@raspberrypi:~ $   /sbin/lspci | grep -i usb

Is highly probably that the USB will be labeled as “sda1”

mariomeraz@raspberrypi:~ $   ls -l /dev/disk/by-uuid

Hint to see real-time how the kernel is recognizing a USB device when the device is connected is the “dmesg” cli command. “dmesg” Displays the kernel messages, this cli command can be useful for finding problems with hardware.

mariomeraz@raspberrypi:~ $ dmesg

[    0.000000] Booting Linux on physical CPU 0x0

[    0.000000] Linux version 5.15.32-v7l+ (dom@buildbot) (arm-linux-gnueabihf-gcc-8 (Ubuntu/Linaro 8.4.0-3ubuntu1) 8.4.0, GNU ld (GNU Binutils for Ubuntu) 2.34) #1538 SMP Thu Mar 31 19:39:41 BST 2022

[    0.000000] CPU: ARMv7 Processor [410fd083] revision 3 (ARMv7), cr=30c5383d

[    0.000000] CPU: div instructions available: patching division code

[    0.000000] CPU: PIPT / VIPT nonaliasing data cache, PIPT instruction cache

[    0.000000] OF: fdt: Machine model: Raspberry Pi 4 Model B Rev 1.5

[    0.000000] random: fast init done

[    0.000000] Memory policy: Data cache writealloc

[    0.000000] Reserved memory: created CMA memory pool at 0x000000001ac00000, size 320 MiB

[    0.000000] OF: reserved mem: initialized node linux,cma, compatible id shared-dma-pool

[    0.000000] Zone ranges:

[    0.000000]   DMA      [mem 0x0000000000000000-0x000000002fffffff]

[    0.000000]   Normal   empty

[    0.000000]   HighMem  [mem 0x0000000030000000-0x00000001ffffffff]

[    0.000000] Movable zone start for each node

[    0.000000] Early memory node ranges

[    0.000000]   node   0: [mem 0x0000000000000000-0x000000003b3fffff]

[    0.000000]   node   0: [mem 0x0000000040000000-0x00000000fbffffff]

[    0.000000]   node   0: [mem 0x0000000100000000-0x00000001ffffffff]

[    0.000000] Initmem setup node 0 [mem 0x0000000000000000-0x00000001ffffffff]

[    0.000000] percpu: Embedded 16 pages/cpu s35788 r8192 d21556 u65536

[    0.000000] pcpu-alloc: s35788 r8192 d21556 u65536 alloc=16*4096

[    0.000000] pcpu-alloc: [0] 0 [0] 1 [0] 2 [0] 3 

[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 2059584

[    0.000000] Kernel command line: coherent_pool=1M 8250.nr_uarts=0 snd_bcm2835.enable_compat_alsa=0 snd_bcm2835.enable_hdmi=1 video=HDMI-A-1:1360x768M@60 smsc95xx.macaddr=E4:5F:01:A0:1C:CC vc_mem.mem_base=0x3ec00000 vc_mem.mem_size=0x40000000  console=ttyS0,115200 console=tty1 root=PARTUUID=e91fd894-02 rootfstype=ext4 fsck.repair=yes rootwait quiet splash plymouth.ignore-serial-consoles

[    0.000000] Unknown kernel command line parameters "splash", will be passed to user space.

[    0.000000] Dentry cache hash table entries: 131072 (order: 7, 524288 bytes, linear)

[    0.000000] Inode-cache hash table entries: 65536 (order: 6, 262144 bytes, linear)

[    0.000000] mem auto-init: stack:off, heap alloc:off, heap free:off

[    0.000000] software IO TLB: mapped [mem 0x0000000012400000-0x0000000016400000] (64MB)

[    0.000000] Memory: 7758764K/8245248K available (10240K kernel code, 1390K rwdata, 3292K rodata, 2048K init, 590K bss, 158804K reserved, 327680K cma-reserved, 7458816K highmem)

[    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=4, Nodes=1

[    0.000000] ftrace: allocating 35355 entries in 104 pages

[    0.000000] ftrace: allocated 104 pages with 3 groups

[    0.000000] trace event string verifier disabled

[    0.000000] rcu: Hierarchical RCU implementation.

[    0.000000]  Rude variant of Tasks RCU enabled.

[    0.000000]  Tracing variant of Tasks RCU enabled.

[    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 10 jiffies.

[    0.000000] NR_IRQS: 16, nr_irqs: 16, preallocated irqs: 16

[    0.000000] GIC: Using split EOI/Deactivate mode

[    0.000000] irq_brcmstb_l2: registered L2 intc (/soc/interrupt-controller@7ef00100, parent irq: 25)

[    0.000000] random: get_random_bytes called from start_kernel+0x574/0x758 with crng_init=1

[    0.000000] arch_timer: cp15 timer(s) running at 54.00MHz (phys).

[    0.000000] clocksource: arch_sys_counter: mask: 0xffffffffffffff max_cycles: 0xc743ce346, max_idle_ns: 440795203123 ns

[    0.000000] sched_clock: 56 bits at 54MHz, resolution 18ns, wraps every 4398046511102ns

[    0.000018] Switching to timer-based delay loop, resolution 18ns

[    0.000315] Console: colour dummy device 80x30

[    0.000383] printk: console [tty1] enabled

[    0.000450] Calibrating delay loop (skipped), value calculated using timer frequency.. 108.00 BogoMIPS (lpj=540000)

[    0.000481] pid_max: default: 32768 minimum: 301

[    0.000622] LSM: Security Framework initializing

[    0.000779] Mount-cache hash table entries: 2048 (order: 1, 8192 bytes, linear)

[    0.000809] Mountpoint-cache hash table entries: 2048 (order: 1, 8192 bytes, linear)

[    0.002376] cgroup: Disabling memory control group subsystem

[    0.002620] CPU: Testing write buffer coherency: ok

[    0.002677] CPU0: Spectre BHB: using loop workaround

[    0.003134] CPU0: thread -1, cpu 0, socket 0, mpidr 80000000

[    0.004382] Setting up static identity map for 0x200000 - 0x20003c

[    0.004590] rcu: Hierarchical SRCU implementation.

[    0.005547] smp: Bringing up secondary CPUs ...

[    0.006747] CPU1: thread -1, cpu 1, socket 0, mpidr 80000001

[    0.006764] CPU1: Spectre BHB: using loop workaround

[    0.008093] CPU2: thread -1, cpu 2, socket 0, mpidr 80000002

[    0.008110] CPU2: Spectre BHB: using loop workaround

[    0.009393] CPU3: thread -1, cpu 3, socket 0, mpidr 80000003

[    0.009411] CPU3: Spectre BHB: using loop workaround

[    0.009567] smp: Brought up 1 node, 4 CPUs

[    0.009589] SMP: Total of 4 processors activated (432.00 BogoMIPS).

[    0.009609] CPU: All CPU(s) started in HYP mode.

[    0.009622] CPU: Virtualization extensions available.

[    0.010513] devtmpfs: initialized

[    0.025979] VFP support v0.3: implementor 41 architecture 3 part 40 variant 8 rev 0

[    0.026220] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns

[    0.026255] futex hash table entries: 1024 (order: 4, 65536 bytes, linear)

[    0.036149] pinctrl core: initialized pinctrl subsystem

[    0.037419] NET: Registered PF_NETLINK/PF_ROUTE protocol family

[    0.042051] DMA: preallocated 1024 KiB pool for atomic coherent allocations

[    0.042857] audit: initializing netlink subsys (disabled)

[    0.043114] audit: type=2000 audit(0.040:1): state=initialized audit_enabled=0 res=1

[    0.043736] thermal_sys: Registered thermal governor 'step_wise'

[    0.044537] hw-breakpoint: found 5 (+1 reserved) breakpoint and 4 watchpoint registers.

[    0.044557] hw-breakpoint: maximum watchpoint size is 8 bytes.

[    0.044967] Serial: AMBA PL011 UART driver

[    0.058663] bcm2835-mbox fe00b880.mailbox: mailbox enabled

[    0.090060] raspberrypi-firmware soc:firmware: Attached to firmware from 2022-03-24T13:19:26, variant start

[    0.100075] raspberrypi-firmware soc:firmware: Firmware hash is e5a963efa66a1974127860b42e913d2374139ff5

[    0.158933] Kprobes globally optimized

[    0.164609] bcm2835-dma fe007000.dma: DMA legacy API manager, dmachans=0x1

[    0.169302] vgaarb: loaded

[    0.169793] SCSI subsystem initialized

[    0.170016] usbcore: registered new interface driver usbfs

[    0.170077] usbcore: registered new interface driver hub

[    0.170695] usbcore: registered new device driver usb

[    0.171106] usb_phy_generic phy: supply vcc not found, using dummy regulator

[    0.171607] pps_core: LinuxPPS API ver. 1 registered

[    0.171623] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>

[    0.171651] PTP clock support registered

[    0.173362] clocksource: Switched to clocksource arch_sys_counter

[    0.254131] VFS: Disk quotas dquot_6.6.0

[    0.254238] VFS: Dquot-cache hash table entries: 1024 (order 0, 4096 bytes)

[    0.254423] FS-Cache: Loaded

[    0.254639] CacheFiles: Loaded

[    0.255707] simple-framebuffer 3e7fe000.framebuffer: framebuffer at 0x3e7fe000, 0x3fc000 bytes

[    0.255730] simple-framebuffer 3e7fe000.framebuffer: format=a8r8g8b8, mode=1360x768x32, linelength=5440

[    0.256223] Console: switching to colour frame buffer device 170x48

[    0.261398] simple-framebuffer 3e7fe000.framebuffer: fb0: simplefb registered!

[    0.271904] NET: Registered PF_INET protocol family

[    0.272155] IP idents hash table entries: 16384 (order: 5, 131072 bytes, linear)

[    0.273834] tcp_listen_portaddr_hash hash table entries: 512 (order: 0, 6144 bytes, linear)

[    0.273868] TCP established hash table entries: 8192 (order: 3, 32768 bytes, linear)

[    0.273935] TCP bind hash table entries: 8192 (order: 4, 65536 bytes, linear)

[    0.274013] TCP: Hash tables configured (established 8192 bind 8192)

[    0.274183] UDP hash table entries: 512 (order: 2, 16384 bytes, linear)

[    0.274222] UDP-Lite hash table entries: 512 (order: 2, 16384 bytes, linear)

[    0.274469] NET: Registered PF_UNIX/PF_LOCAL protocol family

[    0.284315] RPC: Registered named UNIX socket transport module.

[    0.284334] RPC: Registered udp transport module.

[    0.284349] RPC: Registered tcp transport module.

[    0.284363] RPC: Registered tcp NFSv4.1 backchannel transport module.

[    0.284385] PCI: CLS 0 bytes, default 64

[    1.125140] hw perfevents: enabled with armv7_cortex_a7 PMU driver, 7 counters available

[    1.127890] Initialise system trusted keyrings

[    1.128185] workingset: timestamp_bits=14 max_order=21 bucket_order=7

[    1.137433] zbud: loaded

[    1.139443] FS-Cache: Netfs 'nfs' registered for caching

[    1.140283] NFS: Registering the id_resolver key type

[    1.140336] Key type id_resolver registered

[    1.140351] Key type id_legacy registered

[    1.140486] nfs4filelayout_init: NFSv4 File Layout Driver Registering...

[    1.140502] nfs4flexfilelayout_init: NFSv4 Flexfile Layout Driver Registering...

[    1.141636] Key type asymmetric registered

[    1.141653] Asymmetric key parser 'x509' registered

[    1.141880] bounce: pool size: 64 pages

[    1.141947] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 247)

[    1.142180] io scheduler mq-deadline registered

[    1.142196] io scheduler kyber registered

[    1.151487] brcm-pcie fd500000.pcie: host bridge /scb/pcie@7d500000 ranges:

[    1.151527] brcm-pcie fd500000.pcie:   No bus range found for /scb/pcie@7d500000, using [bus 00-ff]

[    1.151623] brcm-pcie fd500000.pcie:      MEM 0x0600000000..0x063fffffff -> 0x00c0000000

[    1.151718] brcm-pcie fd500000.pcie:   IB MEM 0x0000000000..0x01ffffffff -> 0x0400000000

[    1.235463] brcm-pcie fd500000.pcie: link up, 5.0 GT/s PCIe x1 (SSC)

[    1.235831] brcm-pcie fd500000.pcie: PCI host bridge to bus 0000:00

[    1.235852] pci_bus 0000:00: root bus resource [bus 00-ff]

[    1.235874] pci_bus 0000:00: root bus resource [mem 0x600000000-0x63fffffff] (bus address [0xc0000000-0xffffffff])

[    1.235965] pci 0000:00:00.0: [14e4:2711] type 01 class 0x060400

[    1.236212] pci 0000:00:00.0: PME# supported from D0 D3hot

[    1.239966] PCI: bus0: Fast back to back transfers disabled

[    1.239991] pci 0000:00:00.0: bridge configuration invalid ([bus 00-00]), reconfiguring

[    1.240378] pci 0000:01:00.0: [1106:3483] type 00 class 0x0c0330

[    1.240507] pci 0000:01:00.0: reg 0x10: [mem 0x00000000-0x00000fff 64bit]

[    1.240939] pci 0000:01:00.0: PME# supported from D0 D3hot

[    1.244684] PCI: bus1: Fast back to back transfers disabled

[    1.244704] pci_bus 0000:01: busn_res: [bus 01-ff] end is updated to 01

[    1.244749] pci 0000:00:00.0: BAR 8: assigned [mem 0x600000000-0x6000fffff]

[    1.244775] pci 0000:01:00.0: BAR 0: assigned [mem 0x600000000-0x600000fff 64bit]

[    1.244861] pci 0000:00:00.0: PCI bridge to [bus 01]

[    1.244887] pci 0000:00:00.0:   bridge window [mem 0x600000000-0x6000fffff]

[    1.245316] pcieport 0000:00:00.0: enabling device (0140 -> 0142)

[    1.245564] pcieport 0000:00:00.0: PME: Signaling with IRQ 77

[    1.256605] iproc-rng200 fe104000.rng: hwrng registered

[    1.257003] vc-mem: phys_addr:0x00000000 mem_base=0x3ec00000 mem_size:0x40000000(1024 MiB)

[    1.258544] gpiomem-bcm2835 fe200000.gpiomem: Initialised: Registers at 0xfe200000

[    1.271624] brd: module loaded

[    1.282028] loop: module loaded

[    1.282841] Loading iSCSI transport class v2.0-870.

[    1.288276] bcmgenet fd580000.ethernet: GENET 5.0 EPHY: 0x0000

[    1.383515] unimac-mdio unimac-mdio.-19: Broadcom UniMAC MDIO bus

[    1.384779] usbcore: registered new interface driver r8152

[    1.384850] usbcore: registered new interface driver lan78xx

[    1.384913] usbcore: registered new interface driver smsc95xx

[    1.434652] xhci_hcd 0000:01:00.0: xHCI Host Controller

[    1.434692] xhci_hcd 0000:01:00.0: new USB bus registered, assigned bus number 1

[    1.440406] xhci_hcd 0000:01:00.0: hcc params 0x002841eb hci version 0x100 quirks 0x00003c0000000890

[    1.441793] usb usb1: New USB device found, idVendor=1d6b, idProduct=0002, bcdDevice= 5.15

[    1.441817] usb usb1: New USB device strings: Mfr=3, Product=2, SerialNumber=1

[    1.441837] usb usb1: Product: xHCI Host Controller

[    1.441854] usb usb1: Manufacturer: Linux 5.15.32-v7l+ xhci-hcd

[    1.441871] usb usb1: SerialNumber: 0000:01:00.0

[    1.442637] hub 1-0:1.0: USB hub found

[    1.442736] hub 1-0:1.0: 1 port detected

[    1.443469] xhci_hcd 0000:01:00.0: xHCI Host Controller

[    1.443497] xhci_hcd 0000:01:00.0: new USB bus registered, assigned bus number 2

[    1.443525] xhci_hcd 0000:01:00.0: Host supports USB 3.0 SuperSpeed

[    1.443989] usb usb2: New USB device found, idVendor=1d6b, idProduct=0003, bcdDevice= 5.15

[    1.444012] usb usb2: New USB device strings: Mfr=3, Product=2, SerialNumber=1

[    1.444031] usb usb2: Product: xHCI Host Controller

[    1.444048] usb usb2: Manufacturer: Linux 5.15.32-v7l+ xhci-hcd

[    1.444064] usb usb2: SerialNumber: 0000:01:00.0

[    1.444768] hub 2-0:1.0: USB hub found

[    1.444838] hub 2-0:1.0: 4 ports detected

[    1.446679] dwc_otg: version 3.00a 10-AUG-2012 (platform bus)

[    1.447054] dwc_otg: FIQ enabled

[    1.447068] dwc_otg: NAK holdoff enabled

[    1.447082] dwc_otg: FIQ split-transaction FSM enabled

[    1.447100] Module dwc_common_port init

[    1.447586] usbcore: registered new interface driver uas

[    1.447696] usbcore: registered new interface driver usb-storage

[    1.447891] mousedev: PS/2 mouse device common for all mice

[    1.453539] sdhci: Secure Digital Host Controller Interface driver

[    1.453557] sdhci: Copyright(c) Pierre Ossman

[    1.454315] sdhci-pltfm: SDHCI platform and OF driver helper

[    1.458195] ledtrig-cpu: registered to indicate activity on CPUs

[    1.458568] hid: raw HID events driver (C) Jiri Kosina

[    1.458765] usbcore: registered new interface driver usbhid

[    1.458781] usbhid: USB HID core driver

[    1.465468] Initializing XFRM netlink socket

[    1.465512] NET: Registered PF_PACKET protocol family

[    1.465625] Key type dns_resolver registered

[    1.466090] Registering SWP/SWPB emulation handler

[    1.466942] registered taskstats version 1

[    1.466972] Loading compiled-in X.509 certificates

[    1.467864] Key type ._fscrypt registered

[    1.467881] Key type .fscrypt registered

[    1.467895] Key type fscrypt-provisioning registered

[    1.480297] uart-pl011 fe201000.serial: there is not valid maps for state default

[    1.480625] uart-pl011 fe201000.serial: cts_event_workaround enabled

[    1.480759] fe201000.serial: ttyAMA0 at MMIO 0xfe201000 (irq = 34, base_baud = 0) is a PL011 rev2

[    1.490027] bcm2835-wdt bcm2835-wdt: Broadcom BCM2835 watchdog timer

[    1.490572] bcm2835-power bcm2835-power: Broadcom BCM2835 power domains driver

[    1.491865] mmc-bcm2835 fe300000.mmcnr: mmc_debug:0 mmc_debug2:0

[    1.491886] mmc-bcm2835 fe300000.mmcnr: DMA channel allocated

[    1.521024] of_cfs_init

[    1.521272] of_cfs_init: OK

[    1.556747] mmc0: SDHCI controller on fe340000.mmc [fe340000.mmc] using ADMA

[    1.557164] Waiting for root device PARTUUID=e91fd894-02...

[    1.608357] mmc1: new high speed SDIO card at address 0001

[    1.661812] mmc0: new ultra high speed DDR50 SDXC card at address aaaa

[    1.662816] mmcblk0: mmc0:aaaa SR64G 59.5 GiB 

[    1.666109]  mmcblk0: p1 p2

[    1.666663] mmcblk0: mmc0:aaaa SR64G 59.5 GiB

[    1.681550] EXT4-fs (mmcblk0p2): INFO: recovery required on readonly filesystem

[    1.681573] EXT4-fs (mmcblk0p2): write access will be enabled during recovery

[    1.723401] usb 1-1: new high-speed USB device number 2 using xhci_hcd

[    1.785089] EXT4-fs (mmcblk0p2): orphan cleanup on readonly fs

[    1.799881] EXT4-fs (mmcblk0p2): 5 orphan inodes deleted

[    1.799907] EXT4-fs (mmcblk0p2): recovery complete

[    1.906101] usb 1-1: New USB device found, idVendor=2109, idProduct=3431, bcdDevice= 4.21

[    1.906130] usb 1-1: New USB device strings: Mfr=0, Product=1, SerialNumber=0

[    1.906150] usb 1-1: Product: USB2.0 Hub

[    1.908319] hub 1-1:1.0: USB hub found

[    1.908634] hub 1-1:1.0: 4 ports detected

[    1.951438] EXT4-fs (mmcblk0p2): mounted filesystem with ordered data mode. Opts: (null). Quota mode: none.

[    1.951531] VFS: Mounted root (ext4 filesystem) readonly on device 179:2.

[    1.952529] devtmpfs: mounted

[    1.963940] Freeing unused kernel image (initmem) memory: 2048K

[    1.964270] Run /sbin/init as init process

[    1.964285]   with arguments:

[    1.964298]     /sbin/init

[    1.964311]     splash

[    1.964325]   with environment:

[    1.964337]     HOME=/

[    1.964349]     TERM=linux

[    2.233422] usb 1-1.2: new full-speed USB device number 3 using xhci_hcd

[    2.312327] systemd[1]: System time before build time, advancing clock.

[    2.373292] usb 1-1.2: New USB device found, idVendor=248a, idProduct=8367, bcdDevice= 1.00

[    2.373324] usb 1-1.2: New USB device strings: Mfr=1, Product=2, SerialNumber=0

[    2.373380] usb 1-1.2: Product: Wireless Receiver

[    2.373398] usb 1-1.2: Manufacturer: Telink

[    2.403839] input: Telink Wireless Receiver Mouse as /devices/platform/scb/fd500000.pcie/pci0000:00/0000:00:00.0/0000:01:00.0/usb1/1-1/1-1.2/1-1.2:1.0/0003:248A:8367.0001/input/input0

[    2.404419] input: Telink Wireless Receiver Consumer Control as /devices/platform/scb/fd500000.pcie/pci0000:00/0000:00:00.0/0000:01:00.0/usb1/1-1/1-1.2/1-1.2:1.0/0003:248A:8367.0001/input/input1

[    2.425911] NET: Registered PF_INET6 protocol family

[    2.427689] Segment Routing with IPv6

[    2.427763] In-situ OAM (IOAM) with IPv6

[    2.473808] input: Telink Wireless Receiver System Control as /devices/platform/scb/fd500000.pcie/pci0000:00/0000:00:00.0/0000:01:00.0/usb1/1-1/1-1.2/1-1.2:1.0/0003:248A:8367.0001/input/input2

[    2.474160] hid-generic 0003:248A:8367.0001: input,hidraw0: USB HID v1.11 Mouse [Telink Wireless Receiver] on usb-0000:01:00.0-1.2/input0

[    2.481719] input: Telink Wireless Receiver as /devices/platform/scb/fd500000.pcie/pci0000:00/0000:00:00.0/0000:01:00.0/usb1/1-1/1-1.2/1-1.2:1.1/0003:248A:8367.0002/input/input3

[    2.490744] systemd[1]: systemd 247.3-7+rpi1 running in system mode. (+PAM +AUDIT +SELINUX +IMA +APPARMOR +SMACK +SYSVINIT +UTMP +LIBCRYPTSETUP +GCRYPT +GNUTLS +ACL +XZ +LZ4 +ZSTD +SECCOMP +BLKID +ELFUTILS +KMOD +IDN2 -IDN +PCRE2 default-hierarchy=unified)

[    2.491611] systemd[1]: Detected architecture arm.

[    2.493539] systemd[1]: Set hostname to <raspberrypi>.

[    2.544437] hid-generic 0003:248A:8367.0002: input,hidraw1: USB HID v1.11 Keyboard [Telink Wireless Receiver] on usb-0000:01:00.0-1.2/input1

[    2.643516] usb 1-1.4: new low-speed USB device number 4 using xhci_hcd

[    2.781596] usb 1-1.4: New USB device found, idVendor=04f2, idProduct=0939, bcdDevice= 1.00

[    2.781626] usb 1-1.4: New USB device strings: Mfr=1, Product=2, SerialNumber=0

[    2.781647] usb 1-1.4: Product: USB Optical Mouse

[    2.781665] usb 1-1.4: Manufacturer: PixArt

[    2.790906] input: PixArt USB Optical Mouse as /devices/platform/scb/fd500000.pcie/pci0000:00/0000:00:00.0/0000:01:00.0/usb1/1-1/1-1.4/1-1.4:1.0/0003:04F2:0939.0003/input/input4

[    2.791425] hid-generic 0003:04F2:0939.0003: input,hidraw2: USB HID v1.11 Mouse [PixArt USB Optical Mouse] on usb-0000:01:00.0-1.4/input0

[    3.264757] systemd[1]: /lib/systemd/system/plymouth-start.service:16: Unit configured to use KillMode=none. This is unsafe, as it disables systemd's process lifecycle management for the service. Please update your service to use a safer KillMode=, such as 'mixed' or 'control-group'. Support for KillMode=none is deprecated and will eventually be removed.

[    3.458844] systemd[1]: Queued start job for default target Graphical Interface.

[    3.460515] random: systemd: uninitialized urandom read (16 bytes read)

[    3.464850] systemd[1]: Created slice system-getty.slice.

[    3.465306] random: systemd: uninitialized urandom read (16 bytes read)

[    3.466392] systemd[1]: Created slice system-modprobe.slice.

[    3.466525] random: systemd: uninitialized urandom read (16 bytes read)

[    3.467478] systemd[1]: Created slice system-systemd\x2dfsck.slice.

[    3.468394] systemd[1]: Created slice User and Session Slice.

[    3.468996] systemd[1]: Started Forward Password Requests to Wall Directory Watch.

[    3.470168] systemd[1]: Set up automount Arbitrary Executable File Formats File System Automount Point.

[    3.470953] systemd[1]: Reached target Slices.

[    3.471214] systemd[1]: Reached target Swap.

[    3.472290] systemd[1]: Listening on Syslog Socket.

[    3.473104] systemd[1]: Listening on fsck to fsckd communication Socket.

[    3.473619] systemd[1]: Listening on initctl Compatibility Named Pipe.

[    3.474796] systemd[1]: Listening on Journal Audit Socket.

[    3.475608] systemd[1]: Listening on Journal Socket (/dev/log).

[    3.476650] systemd[1]: Listening on Journal Socket.

[    3.484360] systemd[1]: Listening on udev Control Socket.

[    3.485282] systemd[1]: Listening on udev Kernel Socket.

[    3.486198] systemd[1]: Condition check resulted in Huge Pages File System being skipped.

[    3.491691] systemd[1]: Mounting POSIX Message Queue File System...

[    3.498259] systemd[1]: Mounting RPC Pipe File System...

[    3.505773] systemd[1]: Mounting Kernel Debug File System...

[    3.513201] systemd[1]: Mounting Kernel Trace File System...

[    3.514749] systemd[1]: Condition check resulted in Kernel Module supporting RPCSEC_GSS being skipped.

[    3.525089] systemd[1]: Starting Restore / save the current clock...

[    3.534536] systemd[1]: Starting Set the console keyboard layout...

[    3.543067] systemd[1]: Starting Create list of static device nodes for the current kernel...

[    3.551059] systemd[1]: Starting Load Kernel Module configfs...

[    3.558366] systemd[1]: Starting Load Kernel Module drm...

[    3.567297] systemd[1]: Starting Load Kernel Module fuse...

[    3.572379] systemd[1]: Condition check resulted in Set Up Additional Binary Formats being skipped.

[    3.581594] systemd[1]: Starting File System Check on Root Device...

[    3.602030] systemd[1]: Starting Journal Service...

[    3.614404] fuse: init (API version 7.34)

[    3.626057] systemd[1]: Starting Load Kernel Modules...

[    3.634452] systemd[1]: Starting Coldplug All udev Devices...

[    3.650569] systemd[1]: Mounted POSIX Message Queue File System.

[    3.651358] systemd[1]: Mounted RPC Pipe File System.

[    3.652098] systemd[1]: Mounted Kernel Debug File System.

[    3.652879] systemd[1]: Mounted Kernel Trace File System.

[    3.655525] systemd[1]: Finished Restore / save the current clock.

[    3.660435] systemd[1]: Finished Create list of static device nodes for the current kernel.

[    3.662721] systemd[1]: modprobe@configfs.service: Succeeded.

[    3.684929] systemd[1]: Finished Load Kernel Module configfs.

[    3.687532] systemd[1]: modprobe@fuse.service: Succeeded.

[    3.694142] systemd[1]: Finished Load Kernel Module fuse.

[    3.696648] systemd[1]: modprobe@drm.service: Succeeded.

[    3.702702] systemd[1]: Finished Load Kernel Module drm.

[    3.720036] systemd[1]: Mounting FUSE Control File System...

[    3.724216] i2c_dev: i2c /dev entries driver

[    3.729109] systemd[1]: Mounting Kernel Configuration File System...

[    3.737154] systemd[1]: Started File System Check Daemon to report status.

[    3.763466] systemd[1]: Finished Load Kernel Modules.

[    3.764608] systemd[1]: Mounted FUSE Control File System.

[    3.765336] systemd[1]: Mounted Kernel Configuration File System.

[    3.772329] systemd[1]: Starting Apply Kernel Variables...

[    3.864337] systemd[1]: Finished Apply Kernel Variables.

[    3.950883] systemd[1]: Finished File System Check on Root Device.

[    3.957231] systemd[1]: Starting Remount Root and Kernel File Systems...

[    4.032233] systemd[1]: Started Journal Service.

[    4.148110] EXT4-fs (mmcblk0p2): re-mounted. Opts: (null). Quota mode: none.

[    4.216520] systemd-journald[133]: Received client request to flush runtime journal.

[    4.292027] systemd-journald[133]: File /var/log/journal/ec8035161590430d9fc33530696c0cdb/system.journal corrupted or uncleanly shut down, renaming and replacing.

[    5.818439] rpivid-mem feb00000.hevc-decoder: rpivid-hevcmem initialised: Registers at 0xfeb00000 length 0x00010000

[    5.818992] rpivid-mem feb10000.rpivid-local-intc: rpivid-intcmem initialised: Registers at 0xfeb10000 length 0x00001000

[    5.823828] rpivid-mem feb20000.h264-decoder: rpivid-h264mem initialised: Registers at 0xfeb20000 length 0x00010000

[    5.824515] rpivid-mem feb30000.vp9-decoder: rpivid-vp9mem initialised: Registers at 0xfeb30000 length 0x00010000

[    6.092331] vc_sm_cma: module is from the staging directory, the quality is unknown, you have been warned.

[    6.096452] bcm2835_vc_sm_cma_probe: Videocore shared memory driver

[    6.096530] [vc_sm_connected_init]: start

[    6.104520] mc: Linux media interface: v0.10

[    6.124627] [vc_sm_connected_init]: installed successfully

[    6.126868] snd_bcm2835: module is from the staging directory, the quality is unknown, you have been warned.

[    6.167594] videodev: Linux video capture interface: v2.00

[    6.171080] bcm2835_audio bcm2835_audio: card created with 8 channels

[    6.200553] bcm2835_mmal_vchiq: module is from the staging directory, the quality is unknown, you have been warned.

[    6.226698] bcm2835_codec: module is from the staging directory, the quality is unknown, you have been warned.

[    6.232107] bcm2835_isp: module is from the staging directory, the quality is unknown, you have been warned.

[    6.238195] bcm2835-codec bcm2835-codec: Device registered as /dev/video10

[    6.238251] bcm2835-codec bcm2835-codec: Loaded V4L2 decode

[    6.251303] bcm2835-isp bcm2835-isp: Device node output[0] registered as /dev/video13

[    6.251835] bcm2835-isp bcm2835-isp: Device node capture[0] registered as /dev/video14

[    6.252271] bcm2835-isp bcm2835-isp: Device node capture[1] registered as /dev/video15

[    6.252932] bcm2835-isp bcm2835-isp: Device node stats[2] registered as /dev/video16

[    6.252964] bcm2835-isp bcm2835-isp: Register output node 0 with media controller

[    6.252989] bcm2835-isp bcm2835-isp: Register capture node 1 with media controller

[    6.253012] bcm2835-isp bcm2835-isp: Register capture node 2 with media controller

[    6.253034] bcm2835-isp bcm2835-isp: Register capture node 3 with media controller

[    6.267131] bcm2835-isp bcm2835-isp: Device node output[0] registered as /dev/video20

[    6.267633] bcm2835-isp bcm2835-isp: Device node capture[0] registered as /dev/video21

[    6.268063] bcm2835-isp bcm2835-isp: Device node capture[1] registered as /dev/video22

[    6.268423] bcm2835-isp bcm2835-isp: Device node stats[2] registered as /dev/video23

[    6.268454] bcm2835-isp bcm2835-isp: Register output node 0 with media controller

[    6.268479] bcm2835-isp bcm2835-isp: Register capture node 1 with media controller

[    6.268502] bcm2835-isp bcm2835-isp: Register capture node 2 with media controller

[    6.268532] bcm2835-isp bcm2835-isp: Register capture node 3 with media controller

[    6.268746] bcm2835-isp bcm2835-isp: Loaded V4L2 bcm2835-isp

[    6.280404] bcm2835-codec bcm2835-codec: Device registered as /dev/video11

[    6.280456] bcm2835-codec bcm2835-codec: Loaded V4L2 encode

[    6.281547] bcm2835_v4l2: module is from the staging directory, the quality is unknown, you have been warned.

[    6.318093] bcm2835-codec bcm2835-codec: Device registered as /dev/video12

[    6.318151] bcm2835-codec bcm2835-codec: Loaded V4L2 isp

[    6.336139] bcm2835-codec bcm2835-codec: Device registered as /dev/video18

[    6.336193] bcm2835-codec bcm2835-codec: Loaded V4L2 image_fx

[    6.351484] bcm2835-codec bcm2835-codec: Device registered as /dev/video31

[    6.351579] bcm2835-codec bcm2835-codec: Loaded V4L2 encode_image

[    6.365481] checking generic (3e7fe000 3fc000) vs hw (0 ffffffffffffffff)

[    6.365517] fb0: switching to vc4 from simple

[    6.390160] Console: switching to colour dummy device 80x30

[    6.434940] vc4-drm gpu: bound fe400000.hvs (ops vc4_hvs_ops [vc4])

[    6.514502] brcmstb-i2c fef04500.i2c:  @97500hz registered in polling mode

[    6.516764] brcmstb-i2c fef09500.i2c:  @97500hz registered in polling mode

[    6.520620] vc4-drm gpu: bound fe400000.hvs (ops vc4_hvs_ops [vc4])

[    6.557407] Registered IR keymap rc-cec

[    6.557628] rc rc0: vc4 as /devices/platform/soc/fef00700.hdmi/rc/rc0

[    6.557907] input: vc4 as /devices/platform/soc/fef00700.hdmi/rc/rc0/input5

[    6.678091] vc4-drm gpu: bound fe400000.hvs (ops vc4_hvs_ops [vc4])

[    6.709886] Registered IR keymap rc-cec

[    6.710106] rc rc0: vc4 as /devices/platform/soc/fef00700.hdmi/rc/rc0

[    6.710337] input: vc4 as /devices/platform/soc/fef00700.hdmi/rc/rc0/input6

[    6.752893] [drm] Initialized v3d 1.0.0 20180419 for fec00000.v3d on minor 1

[    6.942985] cfg80211: Loading compiled-in X.509 certificates for regulatory database

[    7.004874] cfg80211: Loaded X.509 cert 'sforshee: 00b28ddf47aef9cea7'

[    7.023143] cfg80211: loaded regulatory.db is malformed or signature is missing/invalid

[    7.113294] vc4-drm gpu: bound fe400000.hvs (ops vc4_hvs_ops [vc4])

[    7.139094] Registered IR keymap rc-cec

[    7.221088] rc rc0: vc4 as /devices/platform/soc/fef00700.hdmi/rc/rc0

[    7.221788] input: vc4 as /devices/platform/soc/fef00700.hdmi/rc/rc0/input7

[    7.232598] brcmfmac: F1 signature read @0x18000000=0x15264345

[    7.354229] brcmfmac: brcmf_fw_alloc_request: using brcm/brcmfmac43455-sdio for chip BCM4345/6

[    7.355350] brcmfmac mmc1:0001:1: Direct firmware load for brcm/brcmfmac43455-sdio.raspberrypi,4-model-b.bin failed with error -2

[    7.377203] usbcore: registered new interface driver brcmfmac

[    7.384128] vc4-drm gpu: bound fe400000.hvs (ops vc4_hvs_ops [vc4])

[    7.386284] Registered IR keymap rc-cec

[    7.398327] rc rc0: vc4 as /devices/platform/soc/fef00700.hdmi/rc/rc0

[    7.615394] random: crng init done

[    7.615411] random: 7 urandom warning(s) missed due to ratelimiting

[    7.616415] input: vc4 as /devices/platform/soc/fef00700.hdmi/rc/rc0/input8

[    7.639685] brcmfmac: brcmf_fw_alloc_request: using brcm/brcmfmac43455-sdio for chip BCM4345/6

[    7.639874] brcmfmac: brcmf_fw_alloc_request: using brcm/brcmfmac43455-sdio for chip BCM4345/6

[    7.646195] brcmfmac: brcmf_c_preinit_dcmds: Firmware: BCM4345/6 wl0: Nov  1 2021 00:37:25 version 7.45.241 (1a2f2fa CY) FWID 01-703fd60

[    8.724659] vc4-drm gpu: bound fe400000.hvs (ops vc4_hvs_ops [vc4])

[    8.749819] Registered IR keymap rc-cec

[    8.750021] rc rc0: vc4 as /devices/platform/soc/fef00700.hdmi/rc/rc0

[    8.750332] input: vc4 as /devices/platform/soc/fef00700.hdmi/rc/rc0/input9

[    8.753925] vc4-drm gpu: bound fef00700.hdmi (ops vc4_hdmi_ops [vc4])

[    8.781586] Registered IR keymap rc-cec

[    8.781785] rc rc1: vc4 as /devices/platform/soc/fef05700.hdmi/rc/rc1

[    8.782036] input: vc4 as /devices/platform/soc/fef05700.hdmi/rc/rc1/input10

[    8.828609] vc4-drm gpu: bound fef05700.hdmi (ops vc4_hdmi_ops [vc4])

[    8.829123] vc4-drm gpu: bound fe004000.txp (ops vc4_txp_ops [vc4])

[    8.829736] vc4-drm gpu: bound fe206000.pixelvalve (ops vc4_crtc_ops [vc4])

[    8.830204] vc4-drm gpu: bound fe207000.pixelvalve (ops vc4_crtc_ops [vc4])

[    8.830612] vc4-drm gpu: bound fe20a000.pixelvalve (ops vc4_crtc_ops [vc4])

[    8.830950] vc4-drm gpu: bound fe216000.pixelvalve (ops vc4_crtc_ops [vc4])

[    8.831362] vc4-drm gpu: bound fec12000.pixelvalve (ops vc4_crtc_ops [vc4])

[    8.855596] [drm] Initialized vc4 0.0.0 20140616 for gpu on minor 0

[    8.951137] Console: switching to colour frame buffer device 170x48

[    8.970849] vc4-drm gpu: [drm] fb0: vc4drmfb frame buffer device

[   10.387488] input: BRLTTY 6.3 Linux Screen Driver Keyboard as /devices/virtual/input/input11

[   10.752307] 8021q: 802.1Q VLAN Support v1.8

[   10.886088] uart-pl011 fe201000.serial: no DMA platform data

[   11.117631] Adding 102396k swap on /var/swap.  Priority:-2 extents:2 across:176124k SSFS

[   11.429142] brcmfmac: brcmf_cfg80211_set_power_mgmt: power save enabled

[   12.019126] bcmgenet fd580000.ethernet: configuring instance for external RGMII (RX delay)

[   12.019720] bcmgenet fd580000.ethernet eth0: Link is Down

[   15.832122] systemd-journald[133]: File /var/log/journal/ec8035161590430d9fc33530696c0cdb/user-1000.journal corrupted or uncleanly shut down, renaming and replacing.

[   16.941678] hdmi-audio-codec hdmi-audio-codec.5.auto: ASoC: error at snd_soc_dai_startup on i2s-hifi: -19

[   16.941708]  MAI: soc_pcm_open() failed (-19)

[   16.942496] hdmi-audio-codec hdmi-audio-codec.5.auto: ASoC: error at snd_soc_dai_startup on i2s-hifi: -19

[   16.942522]  MAI: soc_pcm_open() failed (-19)

[   16.943649] hdmi-audio-codec hdmi-audio-codec.5.auto: ASoC: error at snd_soc_dai_startup on i2s-hifi: -19

[   16.943676]  MAI: soc_pcm_open() failed (-19)

[   16.953305] hdmi-audio-codec hdmi-audio-codec.5.auto: ASoC: error at snd_soc_dai_startup on i2s-hifi: -19

[   16.953363]  MAI: soc_pcm_open() failed (-19)

[   16.953928] hdmi-audio-codec hdmi-audio-codec.5.auto: ASoC: error at snd_soc_dai_startup on i2s-hifi: -19

[   16.953955]  MAI: soc_pcm_open() failed (-19)

[   16.954305] hdmi-audio-codec hdmi-audio-codec.5.auto: ASoC: error at snd_soc_dai_startup on i2s-hifi: -19

[   16.954336]  MAI: soc_pcm_open() failed (-19)

[   17.743407] IPv6: ADDRCONF(NETDEV_CHANGE): wlan0: link becomes ready

[   21.172212] Bluetooth: Core ver 2.22

[   21.172331] NET: Registered PF_BLUETOOTH protocol family

[   21.172345] Bluetooth: HCI device and connection manager initialized

[   21.172373] Bluetooth: HCI socket layer initialized

[   21.172392] Bluetooth: L2CAP socket layer initialized

[   21.172426] Bluetooth: SCO socket layer initialized

[   21.184546] Bluetooth: HCI UART driver ver 2.3

[   21.184569] Bluetooth: HCI UART protocol H4 registered

[   21.184662] Bluetooth: HCI UART protocol Three-wire (H5) registered

[   21.184937] Bluetooth: HCI UART protocol Broadcom registered

[   21.436265] Bluetooth: BNEP (Ethernet Emulation) ver 1.3

[   21.436279] Bluetooth: BNEP filters: protocol multicast

[   21.436291] Bluetooth: BNEP socket layer initialized

[   21.452661] NET: Registered PF_ALG protocol family

[   21.490354] cryptd: max_cpu_qlen set to 1000

[   21.633436] Bluetooth: RFCOMM TTY layer initialized

[   21.633461] Bluetooth: RFCOMM socket layer initialized

[   21.633482] Bluetooth: RFCOMM ver 1.11

[   22.158654] ICMPv6: process `dhcpcd' is using deprecated sysctl (syscall) net.ipv6.neigh.wlan0.retrans_time - use net.ipv6.neigh.wlan0.retrans_time_ms instead

[   31.833438] cam-dummy-reg: disabling

[  315.732714] v3d fec00000.v3d: MMU error from client CLE (4) at 0x43c1000, pte invalid

mariomeraz@raspberrypi:~ $

Pipes are an alternative of chaining smaller programs together to accomplish bigger tasks and objectives.

![A picture containing icon Description automatically generated](Images/image00268.jpeg) The stdin, stdout and stderr are standard data streams created when a Linux command is launched, this is the reason why the output is transferred, piped or redirected.

Note: pipe is a form or redirection and transfer of standard output to other destinations.

In Linux each file associated with a process is assigned a unique identificatory. Like these values below:

0: stdin

1: stdout

2: stderr

Stdin —-> Program1 —-> Stdout —->stdin —->Program2—->stdout

The “>” symbol is used to redirect the output of any command

“ls” List contents of the current directory

mariomeraz@raspberrypi:# ls > test.txt

To read the content of a text extension file the less option can be used

mariomeraz@raspberrypi:# less test.text

The cat option (short for concatenate) can be used to dump the entire content of a file to a standard output. This can be useful when it is needed to feed a file into another program or redirect the output to other stdout or stdin.

mariomeraz@raspberrypi:~ $ cat /proc/version

Linux version 5.15.32-v7l+ (dom@buildbot) (arm-linux-gnueabihf-gcc-8 (Ubuntu/Linaro 8.4.0-3ubuntu1) 8.4.0, GNU ld (GNU Binutils for Ubuntu) 2.34) #1538 SMP Thu Mar 31 19:39:41 BST 2022

mariomeraz@raspberrypi:~ $

Processes

![Icon Description automatically generated](Images/image00266.jpeg)

            As in any Linux Operating System or Distro every program on the Raspberry Pi runs an individual and separated process. To monitor the process running a top command can be used, which will display the CPU and memory usage. To list the processes with their id numbers the “ps” command can be used.

“Top” Cli command Displays the programs that are currently using the most CPU time and memory

mariomeraz@raspberrypi:$ top

Performance Information

The “ps” stands for process status and is a powerful tool that provides information about processes running on the Linux system.

To list less information, here is the option pipe can be used for a lot of useful use cases.

mariomeraz@raspberrypi:$ ps -aux | less

mariomeraz@raspberrypi:~ $ ps -aux

USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND

root         1  0.4  0.1  33880  8748 ?        Ss   13:33   0:02 /sbin/init spla

root         2  0.0  0.0      0     0 ?        S    13:33   0:00 [kthreadd]

root         3  0.0  0.0      0     0 ?        I<   13:33   0:00 [rcu_gp]

root         4  0.0  0.0      0     0 ?        I<   13:33   0:00 [rcu_par_gp]

root         6  0.0  0.0      0     0 ?        I<   13:33   0:00 [kworker/0:0H-m

root         7  0.2  0.0      0     0 ?        I    13:33   0:01 [kworker/u8:0-e

root         8  0.0  0.0      0     0 ?        I<   13:33   0:00 [mm_percpu_wq]

root         9  0.0  0.0      0     0 ?        S    13:33   0:00 [rcu_tasks_rude

root        10  0.0  0.0      0     0 ?        S    13:33   0:00 [rcu_tasks_trac

root        11  0.0  0.0      0     0 ?        S    13:33   0:00 [ksoftirqd/0]

root        12  0.0  0.0      0     0 ?        I    13:33   0:00 [rcu_sched]

root        13  0.0  0.0      0     0 ?        S    13:33   0:00 [migration/0]

root        14  0.0  0.0      0     0 ?        S    13:33   0:00 [cpuhp/0]

root        15  0.0  0.0      0     0 ?        S    13:33   0:00 [cpuhp/1]

root        16  0.0  0.0      0     0 ?        S    13:33   0:00 [migration/1]

root        17  0.0  0.0      0     0 ?        S    13:33   0:00 [ksoftirqd/1]

root        20  0.0  0.0      0     0 ?        S    13:33   0:00 [cpuhp/2]

root        21  0.0  0.0      0     0 ?        S    13:33   0:00 [migration/2]

root        22  0.0  0.0      0     0 ?        S    13:33   0:00 [ksoftirqd/2]

root        25  0.0  0.0      0     0 ?        S    13:33   0:00 [cpuhp/3]

root        26  0.0  0.0      0     0 ?        S    13:33   0:00 [migration/3]

root        27  0.0  0.0      0     0 ?        S    13:33   0:00 [ksoftirqd/3]

root        30  0.0  0.0      0     0 ?        S    13:33   0:00 [kdevtmpfs]

root        31  0.0  0.0      0     0 ?        I<   13:33   0:00 [netns]

root        32  0.0  0.0      0     0 ?        I<   13:33   0:00 [inet_frag_wq]

root        33  0.0  0.0      0     0 ?        I    13:33   0:00 [kworker/0:1-ev

root        34  0.0  0.0      0     0 ?        I    13:33   0:00 [kworker/1:1-ev

root        36  0.0  0.0      0     0 ?        I    13:33   0:00 [kworker/3:1-ev

root        37  0.0  0.0      0     0 ?        S    13:33   0:00 [kauditd]

root        38  0.0  0.0      0     0 ?        S    13:33   0:00 [khungtaskd]

root        39  0.0  0.0      0     0 ?        S    13:33   0:00 [oom_reaper]

root        40  0.0  0.0      0     0 ?        I<   13:33   0:00 [writeback]

root        41  0.0  0.0      0     0 ?        S    13:33   0:00 [kcompactd0]

root        61  0.0  0.0      0     0 ?        I<   13:33   0:00 [kblockd]

root        62  0.0  0.0      0     0 ?        I<   13:33   0:00 [blkcg_punt_bio

root        63  0.0  0.0      0     0 ?        S    13:33   0:00 [watchdogd]

root        65  0.0  0.0      0     0 ?        I<   13:33   0:00 [kworker/2:1H-k

root        66  0.0  0.0      0     0 ?        I<   13:33   0:00 [rpciod]

root        68  0.0  0.0      0     0 ?        I<   13:33   0:00 [xprtiod]

root        69  0.0  0.0      0     0 ?        I    13:33   0:00 [kworker/u8:2-e

root        70  0.0  0.0      0     0 ?        S    13:34   0:00 [kswapd0]

root        71  0.0  0.0      0     0 ?        I<   13:34   0:00 [nfsiod]

root        72  0.0  0.0      0     0 ?        I<   13:34   0:00 [kthrotld]

root        74  0.0  0.0      0     0 ?        I<   13:34   0:00 [iscsi_eh]

root        75  0.0  0.0      0     0 ?        I<   13:34   0:00 [iscsi_conn_cle

root        76  0.0  0.0      0     0 ?        I<   13:34   0:00 [nvme-wq]

root        77  0.0  0.0      0     0 ?        I<   13:34   0:00 [nvme-reset-wq]

root        78  0.0  0.0      0     0 ?        I<   13:34   0:00 [nvme-delete-wq

root        80  0.0  0.0      0     0 ?        I<   13:34   0:00 [DWC Notificati

root        81  0.0  0.0      0     0 ?        I<   13:34   0:00 [uas]

root        82  0.3  0.0      0     0 ?        S<   13:34   0:02 [vchiq-slot/0]

root        83  0.1  0.0      0     0 ?        S<   13:34   0:01 [vchiq-recy/0]

root        84  0.0  0.0      0     0 ?        S<   13:34   0:00 [vchiq-sync/0]

root        85  0.0  0.0      0     0 ?        I<   13:34   0:00 [zswap-shrink]

root        86  0.0  0.0      0     0 ?        I    13:34   0:00 [kworker/0:2-ev

root        87  0.0  0.0      0     0 ?        I<   13:34   0:00 [sdhci]

root        88  0.0  0.0      0     0 ?        S    13:34   0:00 [irq/62-mmc0]

root        89  0.0  0.0      0     0 ?        I    13:34   0:00 [kworker/2:2-ev

root        90  0.0  0.0      0     0 ?        I<   13:34   0:00 [mmc_complete]

root        92  0.0  0.0      0     0 ?        I<   13:34   0:00 [kworker/1:1H-k

root        93  0.1  0.0      0     0 ?        I<   13:34   0:00 [kworker/1:2H-k

root        94  0.0  0.0      0     0 ?        S    13:34   0:00 [jbd2/mmcblk0p2

root        95  0.0  0.0      0     0 ?        I<   13:34   0:00 [ext4-rsv-conve

root        97  0.1  0.0      0     0 ?        I<   13:34   0:00 [kworker/3:1H-k

root        98  0.0  0.0      0     0 ?        I<   13:34   0:00 [kworker/3:2H]

root        99  0.0  0.0      0     0 ?        I<   13:34   0:00 [mld]

root       100  0.0  0.0      0     0 ?        I<   13:34   0:00 [ipv6_addrconf]

root       101  0.0  0.0      0     0 ?        I    13:34   0:00 [kworker/1:3-ev

root       116  0.2  0.0      0     0 ?        I<   13:34   0:01 [kworker/0:2H-k

root       133  0.1  0.1  45780 14056 ?        Ss   13:34   0:01 /lib/systemd/sy

root       144  0.0  0.0      0     0 ?        I<   13:34   0:00 [kworker/2:2H-k

root       150  0.0  0.0      0     0 ?        I    13:34   0:00 [kworker/2:3-ev

root       164  0.2  0.0  20364  4940 ?        Ss   13:34   0:01 /lib/systemd/sy

root       194  0.0  0.0      0     0 ?        I    13:34   0:00 [kworker/3:2-ev

root       195  0.0  0.0      0     0 ?        S    13:34   0:00 [vchiq-keep/0]

root       196  0.0  0.0      0     0 ?        S<   13:34   0:00 [SMIO]

root       197  0.0  0.0      0     0 ?        I<   13:34   0:00 [mmal-vchiq]

root       198  0.0  0.0      0     0 ?        I<   13:34   0:00 [mmal-vchiq]

root       199  0.0  0.0      0     0 ?        I<   13:34   0:00 [mmal-vchiq]

root       200  0.0  0.0      0     0 ?        I<   13:34   0:00 [mmal-vchiq]

root       201  0.0  0.0      0     0 ?        I<   13:34   0:00 [mmal-vchiq]

root       203  0.0  0.0      0     0 ?        I<   13:34   0:00 [mmal-vchiq]

root       206  0.0  0.0      0     0 ?        I<   13:34   0:00 [mmal-vchiq]

root       233  0.1  0.0      0     0 ?        S    13:34   0:00 [v3d_bin]

root       237  0.1  0.0      0     0 ?        S    13:34   0:01 [v3d_render]

root       238  0.0  0.0      0     0 ?        S    13:34   0:00 [v3d_tfu]

root       240  0.0  0.0      0     0 ?        S    13:34   0:00 [v3d_csd]

root       241  0.0  0.0      0     0 ?        S    13:34   0:00 [v3d_cache_clea

root       266  0.0  0.0      0     0 ?        I<   13:34   0:00 [cfg80211]

root       285  0.0  0.0      0     0 ?        I<   13:34   0:00 [brcmf_wq/mmc1:

root       304  0.0  0.0      0     0 ?        S    13:34   0:00 [brcmf_wdog/mmc

root       332  0.0  0.0      0     0 ?        I<   13:34   0:00 [kworker/u9:1-b

root       400  0.0  0.0      0     0 ?        S    13:34   0:00 [irq/53-vc4 hdm

root       401  0.0  0.0      0     0 ?        S    13:34   0:00 [irq/54-vc4 hdm

root       402  0.0  0.0      0     0 ?        S    13:34   0:00 [cec-vc4]

root       403  0.0  0.0      0     0 ?        S    13:34   0:00 [irq/50-vc4 hdm

root       404  0.0  0.0      0     0 ?        S    13:34   0:00 [irq/49-vc4 hdm

root       405  0.0  0.0      0     0 ?        S    13:34   0:00 [irq/59-vc4 hdm

root       406  0.0  0.0      0     0 ?        S    13:34   0:00 [irq/60-vc4 hdm

root       407  0.0  0.0      0     0 ?        S    13:34   0:00 [cec-vc4]

root       408  0.0  0.0      0     0 ?        S    13:34   0:00 [irq/56-vc4 hdm

root       409  0.0  0.0      0     0 ?        S    13:34   0:00 [irq/55-vc4 hdm

root       411  0.0  0.0      0     0 ?        S    13:34   0:00 [card0-crtc0]

root       412  0.0  0.0      0     0 ?        S    13:34   0:00 [card0-crtc1]

root       413  0.0  0.0      0     0 ?        S    13:34   0:00 [card0-crtc2]

root       414  0.0  0.0      0     0 ?        S    13:34   0:00 [card0-crtc3]

root       415  0.0  0.0      0     0 ?        S    13:34   0:00 [card0-crtc4]

root       416  0.0  0.0      0     0 ?        S    13:34   0:00 [card0-crtc5]

root       436  0.3  0.1  90292  8524 ?        S<sl 13:34   0:02 /bin/brltty --n

avahi      444  0.0  0.0   6916  2664 ?        Ss   13:34   0:00 avahi-daemon: r

root       445  0.0  0.0   8200  2268 ?        Ss   13:34   0:00 /usr/sbin/cron 

message+   446  0.1  0.0   8032  3896 ?        Ss   13:34   0:00 /usr/bin/dbus-d

avahi      449  0.0  0.0   6756   260 ?        S    13:34   0:00 avahi-daemon: c

root       457  0.0  0.0  40848  7284 ?        Ssl  13:34   0:00 /usr/libexec/po

root       481  0.0  0.0  26544  2872 ?        Ssl  13:34   0:00 /usr/sbin/rsysl

root       498  0.0  0.0  13080  6316 ?        Ss   13:34   0:00 /lib/systemd/sy

nobody     506  0.0  0.0   5312  2248 ?        Ss   13:34   0:00 /usr/sbin/thd -

root       507  0.0  0.1  67940 10092 ?        Ssl  13:34   0:00 /usr/libexec/ud

root       510  0.0  0.0   2876  1840 ?        Ss   13:34   0:00 /usr/sbin/dhcpc

root       518  0.0  0.0  11788  4068 ?        Ss   13:34   0:00 /sbin/wpa_suppl

root       577  0.0  0.0  29532  7080 ?        Ss   13:34   0:00 /usr/sbin/cupsd

root       583  0.0  0.1  57792  8740 ?        Ssl  13:34   0:00 /usr/sbin/Modem

root       589  0.0  0.0  27696    80 ?        SLsl 13:34   0:00 /usr/sbin/rngd 

root       593  0.0  0.0  47588  6112 ?        Ssl  13:34   0:00 /usr/sbin/light

root       617  2.0  0.8 237628 66708 tty7     Ssl+ 13:34   0:11 /usr/lib/xorg/X

root       618  0.0  0.0   8264  3552 tty1     Ss   13:34   0:00 /bin/login -f

lp         620  0.0  0.0  15280  4888 ?        S    13:34   0:00 /usr/lib/cups/n

root       621  0.0  0.0  12056  3552 ?        Ss   13:34   0:00 wpa_supplicant 

root       624  0.0  0.1  42628  8488 ?        Ssl  13:34   0:00 /usr/sbin/cups-

root       652  0.0  0.0  33176  7384 ?        Sl   13:34   0:00 lightdm --sessi

mariome+   657  0.0  0.0  14548  7684 ?        Ss   13:34   0:00 /lib/systemd/sy

mariome+   658  0.0  0.0  36308  2008 ?        S    13:34   0:00 (sd-pam)

mariome+   672  0.0  0.0  26604  4748 ?        S<sl 13:34   0:00 /usr/bin/pipewi

mariome+   673  3.7  0.1 905404 10592 ?        S<sl 13:34   0:21 /usr/bin/pulsea

mariome+   674  0.0  0.1  59908 13004 ?        Ssl  13:34   0:00 /usr/bin/lxsess

rtkit      683  0.0  0.0  24208  2420 ?        SNsl 13:34   0:00 /usr/libexec/rt

mariome+   686  0.0  0.0   7816  3620 ?        Ss   13:34   0:00 /usr/bin/dbus-d

mariome+   694  0.0  0.0  19636  4776 ?        S<l  13:34   0:00 /usr/bin/pipewi

mariome+   717  0.0  0.0   8644  3856 tty1     S+   13:34   0:00 -bash

mariome+   751  0.0  0.0   4616   280 ?        Ss   13:34   0:00 /usr/bin/ssh-ag

root       784  0.0  0.0      0     0 ?        I<   13:34   0:00 [kworker/u9:2-h

root       785  0.0  0.0   2056   116 ?        S    13:34   0:00 /usr/bin/hciatt

root       798  0.0  0.0  21448  7628 ?        Ss   13:34   0:00 /usr/libexec/bl

mariome+   801  0.0  0.0  44272  6140 ?        Ssl  13:34   0:00 /usr/libexec/gv

mariome+   807  0.0  0.0  57032  5040 ?        Sl   13:34   0:00 /usr/libexec/gv

mariome+   820  1.4  0.8 254568 66872 ?        Sl   13:34   0:08 mutter

root       821  0.0  0.0      0     0 ?        I<   13:34   0:00 [cryptd]

mariome+   834  0.0  0.1  49756 10660 ?        Sl   13:34   0:00 lxpolkit

mariome+   841  0.4  0.7 556296 58548 ?        Sl   13:34   0:02 lxpanel --profi

mariome+   846  0.3  0.7 273656 57176 ?        Sl   13:34   0:01 pcmanfm --deskt

mariome+   861 14.2  0.6 121368 51512 ?        Rl   13:34   1:21 /usr/bin/python

mariome+   865  0.0  0.0   4616   280 ?        Ss   13:34   0:00 /usr/bin/ssh-ag

root       866  0.0  0.0      0     0 ?        S<   13:34   0:00 [krfcommd]

mariome+   870  0.0  0.0  47112  5756 ?        Sl   13:34   0:00 /usr/libexec/at

mariome+   888  0.1  0.3  52352 26940 ?        S    13:34   0:00 /usr/bin/python

mariome+   893  0.2  0.0   8480  4236 ?        S    13:34   0:01 /usr/bin/dbus-d

mariome+   924  0.1  0.0  32632  6800 ?        Sl   13:34   0:00 /usr/libexec/at

mariome+   930  0.0  0.0  27172  5372 ?        Sl   13:34   0:00 /usr/lib/menu-c

mariome+   934  0.0  0.1  90416  9248 ?        Ssl  13:34   0:00 /usr/libexec/gv

mariome+   939  0.0  0.0  40824  4456 ?        Ssl  13:34   0:00 /usr/libexec/gv

mariome+   943  0.0  0.0  40844  4704 ?        Ssl  13:34   0:00 /usr/libexec/gv

mariome+   950  0.0  0.0  42360  5168 ?        Ssl  13:34   0:00 /usr/libexec/gv

mariome+   954  0.0  0.0  53304  5484 ?        Ssl  13:34   0:00 /usr/libexec/gv

mariome+   963  0.0  0.0  53732  6812 ?        Sl   13:34   0:00 /usr/libexec/gv

mariome+  1071  1.4  0.1 319968  9316 ?        Sl   13:34   0:08 /usr/lib/speech

mariome+  1077  0.0  0.0 293604  4324 ?        Sl   13:34   0:00 /usr/lib/speech

mariome+  1080  0.3  0.0  27372  3660 ?        Ssl  13:34   0:01 /usr/bin/speech

root      1303  1.0  0.2 105876 19056 ?        Ssl  13:35   0:05 /usr/libexec/pa

mariome+  1460  2.6  0.3 120128 31048 ?        Sl   13:37   0:10 lxterminal

mariome+  1472  0.0  0.0   8624  3836 pts/0    Ss   13:37   0:00 bash

mariome+  1490  0.0  0.0   7800  2856 pts/0    T    13:38   0:00 man ls

mariome+  1500  0.0  0.0   6808   480 pts/0    T    13:38   0:00 pager

root      1517  0.0  0.0      0     0 ?        I    13:39   0:00 [kworker/0:0-ev

root      1518  0.0  0.0      0     0 ?        I    13:39   0:00 [kworker/0:3-ev

root      1541  0.0  0.0      0     0 ?        I    13:39   0:00 [kworker/3:0-mm

root      1547  0.0  0.0      0     0 ?        I<   13:39   0:00 [kworker/3:0H]

root      1550  0.0  0.0      0     0 ?        I    13:39   0:00 [kworker/u8:1-e

mariome+  1564 39.1  1.9 507308 155776 ?       Sl   13:39   1:40 /usr/lib/chromi

root      1585  0.0  0.0      0     0 ?        I<   13:39   0:00 [kworker/2:0H]

root      1586  0.0  0.0      0     0 ?        I<   13:39   0:00 [kworker/1:0H]

mariome+  1588  0.0  0.0  13912  2164 ?        Sl   13:39   0:00 /usr/lib/chromi

root      1590  0.0  0.0      0     0 ?        I<   13:39   0:00 [kworker/0:1H-m

mariome+  1592  0.0  0.0   5700   692 ?        S    13:39   0:00 /usr/lib/chromi

mariome+  1595  0.0  0.4 250684 40284 ?        S    13:39   0:00 /usr/lib/chromi

mariome+  1596  0.0  0.4 250680 39092 ?        S    13:39   0:00 /usr/lib/chromi

mariome+  1598  0.0  0.1 250700 11716 ?        S    13:39   0:00 /usr/lib/chromi

mariome+  1620  7.3  1.3 473604 109444 ?       Sl   13:39   0:18 /usr/lib/chromi

mariome+  1624  0.9  0.8 319556 66524 ?        Sl   13:39   0:02 /usr/lib/chromi

mariome+  1632  0.0  0.4 285932 37832 ?        Sl   13:39   0:00 /usr/lib/chromi

mariome+  1638  0.0  0.2 380548 17352 ?        S    13:39   0:00 /usr/lib/chromi

mariome+  1658  0.0  0.6 347152 51808 ?        Sl   13:39   0:00 /usr/lib/chromi

mariome+  1751  1.2  1.2 408912 103184 ?       Sl   13:39   0:03 /usr/lib/chromi

root      1764  0.1  0.0  53224  6756 ?        Ssl  13:39   0:00 /usr/libexec/up

mariome+  1791 20.9  2.1 505324 177780 ?       Sl   13:39   0:52 /usr/lib/chromi

root      1806  0.0  0.0      0     0 ?        I<   13:39   0:00 [kworker/0:3H-m

root      1817  0.1  0.0      0     0 ?        I    13:39   0:00 [kworker/u8:3-e

root      1818  0.0  0.0      0     0 ?        I    13:40   0:00 [kworker/2:0-mm

root      1829  0.0  0.0      0     0 ?        I    13:41   0:00 [kworker/1:0-ev

systemd+  1908  0.0  0.0  22288  2640 ?        Ssl  13:41   0:00 /lib/systemd/sy

mariome+  1978  0.8  0.0  11352  2948 pts/0    S+   13:41   0:01 top

mariome+  2066  0.0  0.0   8624  3804 pts/1    Ss   13:42   0:00 bash

mariome+  2077  0.6  0.0  11352  2984 pts/1    T    13:42   0:00 top

mariome+  2093  0.0  0.0  10860  2596 pts/1    R+   13:43   0:00 ps -aux

mariomeraz@raspberrypi:~ $ 

The sequence below printout CPU information

mariomeraz@raspberrypi:~ $ cat /proc/cpuinfo

processor : 0

model name : ARMv7 Processor rev 4 (v7l)

BogoMIPS : 76.80

Features : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32 

CPU implementer : 0x41

CPU architecture: 7

CPU variant : 0x0

CPU part : 0xd03

CPU revision : 4

processor : 1

model name : ARMv7 Processor rev 4 (v7l)

BogoMIPS : 76.80

Features : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32 

CPU implementer : 0x41

CPU architecture: 7

CPU variant : 0x0

CPU part : 0xd03

CPU revision : 4

processor : 2

model name : ARMv7 Processor rev 4 (v7l)

BogoMIPS : 76.80

Features : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32 

CPU implementer : 0x41

CPU architecture: 7

CPU variant : 0x0

CPU part : 0xd03

CPU revision : 4

processor : 3

model name : ARMv7 Processor rev 4 (v7l)

BogoMIPS : 76.80

Features : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32 

CPU implementer : 0x41

CPU architecture: 7

CPU variant : 0x0

CPU part : 0xd03

CPU revision : 4

Hardware : BCM2835

Revision : a02082

Serial : 000000007b72c055

Model : Raspberry Pi 3 Model B Rev 1.2

mariomeraz@raspberrypi:~ $ 

Whenever is needed to kill any unresponsive process the kill option can be used after to find out the process id with the command “ps”, for example

mariomeraz@raspberrypi:$ kill 6077

![Icon Description automatically generated](Images/image00266.jpeg)

More ways to fetch Linux knowledge

These two commands below are super important to increase the knowledge of the Linux commands options.

The cli command “Man” provides the complete description and options of a command

mariomeraz@raspberrypi:$ man ls

Help typed as below will provide the options available of any command

mariomeraz@raspberrypi:$ ls - - help

mariomeraz@raspberrypi:~ $ ls --help

Usage: ls [OPTION]... [FILE]...

List information about the FILEs (the current directory by default).

Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options too.

  -a, --all                  do not ignore entries starting with .

  -A, --almost-all           do not list implied . and ..

      --author               with -l, print the author of each file

  -b, --escape               print C-style escapes for nongraphic characters

      --block-size=SIZE      with -l, scale sizes by SIZE when printing them;

                               e.g., '--block-size=M'; see SIZE format below

  -B, --ignore-backups       do not list implied entries ending with ~

  -c                         with -lt: sort by, and show, ctime (time of last

                               modification of file status information);

                               with -l: show ctime and sort by name;

                               otherwise: sort by ctime, newest first

  -C                         list entries by columns

      --color[=WHEN]         colorize the output; WHEN can be 'always' (default

                               if omitted), 'auto', or 'never'; more info below

  -d, --directory            list directories themselves, not their contents

  -D, --dired                generate output designed for Emacs' dired mode

  -f                         do not sort, enable -aU, disable -ls --color

  -F, --classify             append indicator (one of */=>@|) to entries

      --file-type            likewise, except do not append '*'

      --format=WORD          across -x, commas -m, horizontal -x, long -l,

                               single-column -1, verbose -l, vertical -C

      --full-time            like -l --time-style=full-iso

  -g                         like -l, but do not list owner

      --group-directories-first

                             group directories before files;

                               can be augmented with a --sort option, but any

                               use of --sort=none (-U) disables grouping

  -G, --no-group             in a long listing, don't print group names

  -h, --human-readable       with -l and -s, print sizes like 1K 234M 2G etc.

      --si                   likewise, but use powers of 1000 not 1024

  -H, --dereference-command-line

                             follow symbolic links listed on the command line

      --dereference-command-line-symlink-to-dir

                             follow each command line symbolic link

                               that points to a directory

      --hide=PATTERN         do not list implied entries matching shell PATTERN

                               (overridden by -a or -A)

      --hyperlink[=WHEN]     hyperlink file names; WHEN can be 'always'

                               (default if omitted), 'auto', or 'never'

      --indicator-style=WORD  append indicator with style WORD to entry names:

                               none (default), slash (-p),

                               file-type (--file-type), classify (-F)

  -i, --inode                print the index number of each file

  -I, --ignore=PATTERN       do not list implied entries matching shell PATTERN

  -k, --kibibytes            default to 1024-byte blocks for disk usage;

                               used only with -s and per directory totals

  -l                         use a long listing format

  -L, --dereference          when showing file information for a symbolic

                               link, show information for the file the link

                               references rather than for the link itself

  -m                         fill width with a comma separated list of entries

  -n, --numeric-uid-gid      like -l, but list numeric user and group IDs

  -N, --literal              print entry names without quoting

  -o                         like -l, but do not list group information

  -p, --indicator-style=slash

                             append / indicator to directories

  -q, --hide-control-chars   print ? instead of nongraphic characters

      --show-control-chars   show nongraphic characters as-is (the default,

                               unless program is 'ls' and output is a terminal)

  -Q, --quote-name           enclose entry names in double quotes

      --quoting-style=WORD   use quoting style WORD for entry names:

                               literal, locale, shell, shell-always,

                               shell-escape, shell-escape-always, c, escape

                               (overrides QUOTING_STYLE environment variable)

  -r, --reverse              reverse order while sorting

  -R, --recursive            list subdirectories recursively

  -s, --size                 print the allocated size of each file, in blocks

  -S                         sort by file size, largest first

      --sort=WORD            sort by WORD instead of name: none (-U), size (-S),

                               time (-t), version (-v), extension (-X)

      --time=WORD            change the default of using modification times;

                               access time (-u): atime, access, use;

                               change time (-c): ctime, status;

                               birth time: birth, creation;

                             with -l, WORD determines which time to show;

                             with --sort=time, sort by WORD (newest first)

      --time-style=TIME_STYLE  time/date format with -l; see TIME_STYLE below

  -t                         sort by time, newest first; see --time

  -T, --tabsize=COLS         assume tab stops at each COLS instead of 8

  -u                         with -lt: sort by, and show, access time;

                               with -l: show access time and sort by name;

                               otherwise: sort by access time, newest first

  -U                         do not sort; list entries in directory order

  -v                         natural sort of (version) numbers within text

  -w, --width=COLS           set output width to COLS.  0 means no limit

  -x                         list entries by lines instead of by columns

  -X                         sort alphabetically by entry extension

  -Z, --context              print any security context of each file

  -1                         list one file per line.  Avoid '\n' with -q or -b

      --help     display this help and exit

      --version  output version information and exit

The SIZE argument is an integer and optional unit (example: 10K is 10*1024).

Units are K,M,G,T,P,E,Z,Y (powers of 1024) or KB,MB,... (powers of 1000).

Binary prefixes can be used, too: KiB=K, MiB=M, and so on.

The TIME_STYLE argument can be full-iso, long-iso, iso, locale, or +FORMAT.

FORMAT is interpreted like in date(1).  If FORMAT is FORMAT1<newline>FORMAT2,

then FORMAT1 applies to non-recent files and FORMAT2 to recent files.

TIME_STYLE prefixed with 'posix-' takes effect only outside the POSIX locale.

Also the TIME_STYLE environment variable sets the default style to use.

Using color to distinguish file types is disabled both by default and

with --color=never.  With --color=auto, ls emits color codes only when

standard output is connected to a terminal.  The LS_COLORS environment

variable can change the settings.  Use the dircolors command to set it.

Exit status:

 0  if OK,

 1  if minor problems (e.g., cannot access subdirectory),

 2  if serious trouble (e.g., cannot access command-line argument).

GNU coreutils online help: <https://www.gnu.org/software/coreutils/>

Full documentation <https://www.gnu.org/software/coreutils/ls>

or available locally via: info '(coreutils) ls invocation'

mariomeraz@raspberrypi:~ $ 

# General Purpose Input Output (GPIO)

The General-Purpose Input Output (GPIO) are intended to be used to interact with hardware connecting the Raspberry pi to low level peripherals. These pins can be controlled from any development environment or programming language based on functionalities and requirements. The GPIOs are the interface with the real world. The GPIO Pins function has changed among different Raspberry Pi versions, for instance on the raspberry pi version 1 we there are 26 Pins, whereas in the raspberry pi version 4 there’re 40 Pins. The GPIO pins are standard designed to control input and output behavior with all kinds of integrated circuits. The very top row of pins is designed to offer power to external devices. Also, there are several ground pins located in the GPIO port.

![A picture containing text, electronics, circuit Description automatically generated](Images/image00293.jpeg)

| GPIO | Specification | Description |
| 3V3 | 3.3 volts | Anything connected to these pins will always get 3.3V of power |
| 5V | 5 volts | Anything connected to these pins will always get 5V of power |
| GND | ground | Zero volts, used to complete a circuit |
| GP2 | GPIO pin 2 | These pins are for general-purpose use and can be configured as input or output pins |
| ID_SC/ID_SD/DNC | Special purpose pins |  |

Naming Conventions

All the GPIO ports are multipurpose, some pins are reserved for 5V, 3.3V and ground. There are other GPIO ports with special capabilities. There are some especial naming conventions like GPIO 18, also known as pin 12 and PCM_CLK. This pin is capable of hardware pulse-width modulation (PWM), and normally this port is used for controlling LED lights and motors among other things.

The pin-naming conventions that is commonly used in the Python scripts can be set manually. BCM (Broadcom) Pin Name or the physical pin locations (BOARD) can be set. The best practice to deal with the GPIO pin-naming issues is to choose a convention and stick with it. For instance: GPIO.setmode (GPIO.BCM)

To use one of these packages below it is needed to download the code, configure the package and install it.

| Module | Description | URL | Package Name |
| RPi.GPIO | GPIO Pins | https://sourceforge.net/projects/raspberry-gpio-python/ | Python-rpi.gpio |
| SimpleCV | Easy API for Computer Vision | http://simplecv.org/ |  |
| Scipy | Scientific Computing | https://scipy.org/download/ | Python-scipy |
| Flask | Microframework for web development | https://flask.palletsprojects.com/en/2.1.x/ | Python-flask |
| Pygame | Gaming Framework | https://www.pygame.org/wiki/GettingStarted | Python-pygame |
| WxPython | GUI framework | https://wxpython.org/ | Python-wxgtk2.8 |
| PySerial | Access to serial ports | https://pyserial.readthedocs.io/en/latest/ | Python-serial |
| PyUSB | FTDI-USB interface | https://pypi.org/project/pyusb/ |  |

mariomeraz@raspberrypi: ~$ pinout

,--------------------------------.

| oooooooooooooooooooo J8     +====

| 1ooooooooooooooooooo        | USB

|                             +====

|      Pi Model 3B  V1.2         |

|      +----+                 +====

| |D|  |SoC |                 | USB

| |S|  |    |                 +====

| |I|  +----+                    |

|                   |C|     +======

|                   |S|     |   Net

| pwr        |HDMI| |I||A|  +======

`-| |--------|    |----|V|-------'

Revision           : a02082

SoC                : BCM2837

RAM                : 1024Mb

Storage            : MicroSD

USB ports          : 4 (excluding power)

Ethernet ports     : 1

Wi-fi              : True

Bluetooth          : True

Camera ports (CSI) : 1

Display ports (DSI): 1

J8:

   3V3  (1) (2)  5V    

 GPIO2  (3) (4)  5V    

 GPIO3  (5) (6)  GND   

 GPIO4  (7) (8)  GPIO14

   GND  (9) (10) GPIO15

GPIO17 (11) (12) GPIO18

GPIO27 (13) (14) GND   

GPIO22 (15) (16) GPIO23

   3V3 (17) (18) GPIO24

GPIO10 (19) (20) GND   

 GPIO9 (21) (22) GPIO25

GPIO11 (23) (24) GPIO8 

   GND (25) (26) GPIO7 

 GPIO0 (27) (28) GPIO1 

 GPIO5 (29) (30) GND   

 GPIO6 (31) (32) GPIO12

GPIO13 (33) (34) GND   

GPIO19 (35) (36) GPIO16

GPIO26 (37) (38) GPIO20

   GND (39) (40) GPIO21

For further information, please refer to https://pinout.xyz/

mariomeraz@raspberrypi: ~$

The GPIO pins on the Raspberry Pi can be controlled and triggered in many ways. GPIO pins can be controlled through designed modules from programming languages.

Since Python is the official language of the Raspberry Pi, there are GPIO modules for python which provide control for inputs and outputs available. The library is called RPi.GPIO and is installed by default on all Raspberry Pi. This python capabilities are a project hosted on SourceForge and can be found at sourceforge.net/project/raspberry-gpio-python

![Graphical user interface, website Description automatically generated](Images/image00294.jpeg)

Further documentation on Python can be found at [www.python.org/doc](http://www.python.org/doc)

RPi. GPIO Installation

mariomeraz@raspberrypi: ~$ sudo apt-get install python-dev

mariomeraz@raspberrypi: ~$sudo apt-get install python-rpi.gpio

# Python the Basics

![Icon Description automatically generated](Images/image00269.jpeg)

Python is an important language, is that important that is used by Science, Tech Industry, and even Hackers consider python as the preferred programing language. Guido van Rossum is the name of the creator of Python. In 1999, van Rossum put together a widely read proposal called Computer Programming for Everybody: [https://www.python.org/doc/essays/cp4e/](https://www.python.org/doc/essays/cp4e/)

Python is an interpreted language which means  the source code of a Python program is converted into bytecode that is then executed by the Python virtual machine. Interpreted language in simple terms means running code line by line but also means that the instruction is executed without earlier compiling the whole program into machine language, although here is a little secret: Python is both compiled as well as an interpreted language.

This means when the  python code is processed, it is first compiled and then interpreted line by line. The compilation part is mostly hidden from the user. While running the code, Python generates a byte code internally, this byte code is then converted using a python virtual machine (p.v.m) to generate the output. The compile part gets deleted as soon as the code gets executed in Python so that the programmer doesn’t get onto unnecessary complexity. Due to al that mentioned the size of programs written in Python is less, and it is easier to debug the code in the Python language. Although the program that is executed in an interpreted language is slower as compared to a language that is directly compiled because the line of codes passes through an interpretation run-time which increases the run-time complexity, for instance in a python program there isn’t a need to specify to the computer whether a variable is a number a list or a string; the interpreter figures out the data types when the program or script is executed.

![A picture containing icon Description automatically generated](Images/image00268.jpeg) And this is one of the capacities why Hackers prefer the use of python precisely for this variable flexibility performed by interpreter.

Let’s start with our first script in Python and in order to do that we need to open the tool that we will use to build the python scripts and programs which is an integrated development environment. The IDE is a software application that helps programmers develop software code efficiently, because it increases developer productivity by combining capabilities such as software editing, building, testing, and packaging in an easy-to-use application.

The IDE that we will use for python that comes with the Raspberry OS called “Thonny Python IDE”, therefore let’s follow the instructions below

Click on the Raspberry Symbol -> ![](Images/image00287.jpeg)Then Go to Programing{Which is the First Option} -> Then Go to Thonny Python IDE and you will see the screen below

![Graphical user interface, text, application, email Description automatically generated](Images/image00295.jpeg)

For more information on “ Thonny Python IDE” [https://thonny.org/](https://thonny.org/)

Python First Steps

Once that we open Thonny the triple chevron (>>>) is the interactive prompt, which means the interpreter is waiting for the instructions.

Let’s follow these steps:

Type the following:

>>> print (“ Hello World”)

Hit Enter, then python will execute the statement.

Result:

>>> Hola World

![Icon Description automatically generated](Images/image00269.jpeg)![A picture containing icon Description automatically generated](Images/image00268.jpeg) What are Imports in Python?

Importing refers to allowing a Python file or a Python module to access the script from another Python file or module. Imports in Python are important for structuring your code effectively.

There are generally three groups:

Standard library imports: Python's built-in modules

Third party imports: Modules that are installed and do not belong to the current application.

Local application imports: Modules that belong to the current application

Example with imports

>>> import math

>>> radius = 200

>>> radius *2 *math.pi

1256.6370614359173

>>> 

![Icon Description automatically generated](Images/image00296.jpeg)

 ![Icon Description automatically generated](Images/image00267.jpeg)

Edit Options in Thonny Python

Indentation is Important for Python. Indentation refers to the spaces at the beginning of a code line. Where in other programming languages the indentation in code is for readability only, although the indentation in Python is very important. Python uses indentation to indicate a block of code.

The indentations errors are pointed out as below:

       ^

IndentationError: expected an indented block

To start a new program, select File -> New Window and Thonny will provide the scrip editing window

The Files, Scripts, and python programs are saved with the extension (.py)

Example:

NewScript.py

To run this script in the terminal it is needed to type the following

mariomeraz@raspberrypi:~ $ python NewScript.py

In my opinion if you reached to this point, then you are ready to start putting together projects, since you have already gone through the basic mechanics and more to understand Linux environments, basic python principles and fundamental concepts to create projects, remember the sky is the limit.

Python Object and Modules

In python the strings, lists, functions, modules and even numbers are objects. A python object can be conceptualized as an encapsulated collection of attributes and methods. An object is a combination of data and behaviors that has a name.  Python is a clean language with 34 reserved keywords. These keywords in the table below are the core part of the language that let you structure and control the flow of activities in a python script. Everything that isn’t a keyword can be considered an object.

Python 34 Reserved Keywords

| CONDITIONALS | CLASSES,FUNCTIONS,MODULES | ERROR HANDLING | LOOPS | BUILD-INFUNCTIONS |
| And | Class | Try | As | Del |
| Else | Def | Except | Break | Pass |
| Elif | Global | Finally | Continue | Print |
| Not | Lambda | Raise | In |  |
| Or | Nonlocal | Assert | For |  |
| If | From | With | While |  |
| Is | Import |  |  |  |
| True | Return |  |  |  |
| False | Yield |  |  |  |
| None |  |  |  |  |

![Icon Description automatically generated](Images/image00266.jpeg)

The Help () instruction provides information about the topics with the options below:

>>>  help (“print”)

>>>  help (“topics”)

>>>  help (“keywords”)

>>>  help (“modules”)

#  All about Raspberry pi Projects

There is a lot to discuss in this chapter, this is all about the projects that you will be able to put together whit the Raspberry pi , a prototype board, a couple of cables, some sensors, and peripherals such as displays and the raspberry-pi camera and voila!! Your projects will be brought to life.

This mini touch screen (features a 2.8" display with 320x240) which is being sold in Amazon or other places and it is very simple to put it together, it is just a matter of ensembled it and insert the SD card with image of the operating system.

![A picture containing text, electronics Description automatically generated](Images/image00297.jpeg)

GitHub

GitHub is an Internet hosting service for software development and version control using Git. It provides the distributed version control of Git plus access control, bug tracking, software feature requests, task management, continuous integration, and wikis for every project.

We will use github just as an additional tool for the people who would like to copy the code of the projects the main link is the one below:

[https://github.com/mariomeraztechauthor/Linux_Raspberrypi_Book](https://github.com/mariomeraztechauthor/Linux_Raspberrypi_Book)

![Graphical user interface, text, application, website Description automatically generated](Images/image00298.jpeg)

Disclaimer

The content in this book is for educational purposes only. The software, code and scripts in this book are provided “as is” without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose and noninfringement. In no event shall the author of this book (Mario Meraz) is liable for any claim, damages or other liability, whether in an action of contract, tort or otherwise, arising from, out of or in connection with the software or use or other dealings in the software, code and scripts here presented in the book the github links and the web site: [www.mariomerazauthor.com](http://www.mariomerazauthor.com)

## What is the internet of Things (IoT) ?

According to Wikipedia: The internet of things is the network of physical devices, vehicles, home appliances and many other items embedded with electronics, software, sensors, actuators, and network connectivity which enable these objects to connect and exchange data.

Sensor

[Data Collection & Measurement]

Wired or Wireless Network

[Transmission of Data through network]

Server

[Data Assessment]

User Interaction

[Action or response based on assessment]

The IoT technologies are nowadays everywhere, and the ecosystem is rich and extended to almost all industries, these days currently things as streets lights, trash cans, containers, caws, cars, smartwatch’s ,  medical devices, smart grids, makers-types small boards such as Arduino and raspberry are considered IoT devices as well, needless to say trees are connected to the internet of things networks.

There are estimations that by 2025 around 20 billion of IoT will be connected to any type of network either private or public network such as the internet.

Reference: IoT & 5G Architectures and Standards.

Internet of Things, 5G Open RAN, 3GPP Standards & Industry 4.0, by Mario Meraz

Let’s start off with the types of sensors. There are several types of sensors, which we will define below:

Digital Sensors & IoT

Here is where we will discuss the projects that are IoT (Internet of Things) Projects since through sensors we can bring sensed measurements to the internet.

A digital sensor is an electronic or electrochemical sensor. Sensors are being used in many IoT applications to collect external values, where data is digitally converted and transmitted. Sensors are often used for analytical measurements, for example the measurement of temperatures, chemical and physical properties of liquids. Typical measured parameters are pH value, [conductivity](https://en.wikipedia.org/wiki/Electrical_conductivity), oxygen, or even “redox potentials” which is a measure of the ease with which a molecule will accept electrons and others.

One Wire Sensors

1-Wire is similar in concept to I²C, but with lower data rates and longer range. It is typically used to communicate with small inexpensive devices such as digital thermometers and weather instruments among other sensors that require minimal wiring.

The CLI command to confirm 1-wire is working properly is the one below:

mariomeraz@raspberrypi:  ~ $ ls /sys/bus/w1/devices

00-480000000000  00-880000000000  00-c80000000000  w1_bus_master1

mariomeraz@raspberrypi:  ~ $ 

1-Wire Data Transmission Advantages and Disadvantages

Advantages

*   Only requires one GPIO pin 
*   One Data Wire (plus ground and possibly voltage)
*   Log Range (200 meters)
*   Inexpensive
*   Minimal wiring
*   16.3 kbps

Disadvantages

*   Low Speed
*   Parasitic Power
*   Some 1-Wire devices can use Voltage on Data line to charge
*   Requires an onboard battery or capacitor to store the charge
*   Requires enough “data-on” to supply voltage (data-off will not charge)
*   One -Wire GPIO - 7 

I2C Sensor

The I2C bus is a simple and flexible way to transfer digital data between two electronic devices which may be physically separate or contained on the same printed circuit board (PCB).

I2C devices exchange bits of data whenever the shared clock signal changes. Controllers and peripheral devices both send bits of data when the clock changes from low to high (called the rising edge of the clock). Unlike with SPI, they cannot send data at the same time. I2C or Inter-Integrated Circuit, is a simple communication protocol often used in embedded systems to transfer data between a master (or multiple masters) and a single slave (or multiple slaves) device. It is a bidirectional two-wire serial bus that uses serial clock (SCL) in synchronous communication and serial data (SDA) wires to send and manage data bit by bit between devices connected to the bus. The standard data transfer rate of the I2C protocol is 100 kbps, although data speeds of up to 5 Mbps are possible with I2C devices configured in "fast mode" or "ultra-fast mode".

SPI Sensor

Serial Peripheral Interface is a serial communication protocol often used in embedded systems for high-speed data exchanges between devices on the bus. It operates using a master-slave paradigm that includes at least four signals: a clock (SCLK), a master output/slave input (MOSI), a master input/slave output (MISO), and a slave select (SS) signal. The SCLK, MOSI, and MISO signals are shared by all devices on the bus. The SCLK signal is generated by the master device for synchronization, while the MOSI and MISO lines are used for data exchange. SPI communication supports full-duplex communication, meaning that both the master and slave can transmit data simultaneously. The exchange itself has no pre-defined protocol which makes SPI ideal for data-streaming applications. It also has no maximum speed; data speeds of more than 100 MHz have been achieved.

I2C is a two-wire protocol and SPI is a four-wire protocol. I2C supports clock stretching and SPI does not have clock stretching. I2C is slower than SPI. I2C has extra overhead start and stop bits and SPI does not have any start and stop bits.

Serial (UART) Sensor

UART, or Universal Asynchronous Receiver/ Transmitter, is a physical circuit in a microcontroller or single integrated circuit (IC) that is used to implement serial communication between devices in an embedded system. Essentially, a UART’s main purpose is to transmit and receive serial data. This serial data is transmitted to the UART on the receiver device, or the receiving UART. The receiving UART converts the received serial data back to parallel data and sends it to the CPU. For UART to convert serial-to-parallel and parallel-to-serial data, shift registers on the transmitting and receiving UART are used. In UART communication, only two wires are required for communication: data flows from the Tx pin of the transmitting UART (Transmitter Tx) to the Rx pin of the receiving UART (Receiver Rx).

UART data is sent over the bus in the form of a packet. A packet consists of a start bit, data frame, a parity bit, and stop bits. The parity bit is used as an error check mechanism to help ensure data integrity. UART is considered to be “universal” because the parameters including transfer speed and data speed are configurable by the developer.

UART supports bidirectional data transmission, including half-duplex and full-duplex operations. It is also asynchronous, meaning it doesn’t use a clock signal to synchronize the output bits from the transmitting UART to the sampling bits on the receiving UART. Without a clock, the receiving and transmitting UART need to be on the same baud rate, or bit rate. This allows the system to know where and when the bits have been clocked.

SPI is much faster in speed compared to UART and I2C. Although UART is often used as a form of device-to-device communication in computer and microcontroller applications.

Reference

[https://www.totalphase.com/blog/2021/12/i2c-vs-spi-vs-uart-introduction-and-comparison-similarities-differences/](https://www.totalphase.com/blog/2021/12/i2c-vs-spi-vs-uart-introduction-and-comparison-similarities-differences/)

![Icon Description automatically generated](Images/image00267.jpeg) Something that is important before start to work with sensors, protocols and interfaces is to enable the ones that will be used

Click on the Raspberry Symbol -> ![](Images/image00287.jpeg)Then Go to Preferences -> Then Go to Raspberry Pi Configuration and then select the Interfaces tab , therefore you will see the screen below

![Graphical user interface, table Description automatically generated](Images/image00299.jpeg)

## Project with python and OLED Display

This project is basically the first project with interaction with hardware, basically is the version of the “Hello World” but with the combination of Linux raspberry pi, an OLED Display and python code.

Let’s start with the installation of the build-essential python, but we need to define what it is a build-essential.

What is build-essential Python?

Build-essential is what is called a meta-package. It does not install anything. Instead, it is a link to several other packages that will be installed as dependencies. In the case of the build-essential meta-package, it will install everything required for compiling basic software written in C and C++.

mariomeraz@raspberrypi:  ~ $sudo apt install build-essential python-dev

Reading package lists... Done

Building dependency tree       

Reading state information... Done

build-essential is already the newest version (12.6).

python-dev is already the newest version (2.7.16-1).

python-dev set to manually installed.

The following packages were automatically installed and are no longer required:

  libmicrodns0 rpi-eeprom-images

Use 'sudo apt autoremove' to remove them.

0 upgraded, 0 newly installed, 0 to remove and 224 not upgraded.

The OLED display (0.96 inch)

The organic light-emitting diode (OLED) display that we’ll use in this tutorial is the SSD1306 model: a mono-color, 0.96-inch display with 128×64 pixels as shown in the following figure.

The OLED display doesn’t require a backlight, which results in a very nice contrast in dark environments. Additionally, its pixels consume energy only when they are on, so the OLED display consumes less power when compared with other displays. The model we are using here has only four pins and communicates with the Arduino using I2C communication protocol. There are models that come with an extra RESET pin. There are also other OLED displays that communicate using SPI communication.

An organic light-emitting diode (OLED or organic LED), also known as organic electroluminescent (organic EL) diode, is a light-emitting diode (LED).

[https://pypi.org/project/luma.oled/](https://pypi.org/project/luma.oled/)

![A picture containing electronics Description automatically generated](Images/image00300.jpeg)  ![Graphical user interface, application Description automatically generated](Images/image00301.jpeg)

To identify the address of the OLED i2c device, the cli instruction sort of debug command needs to be issued

mariomeraz@raspberrypi:~ $ i2cdetect -y 1

     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f

00:          -- -- -- -- -- -- -- -- -- -- -- -- -- 

10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 

20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 

30: -- -- -- -- -- -- -- -- -- -- -- -- 3c -- -- -- 

40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 

50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 

60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 

70: -- -- -- -- -- -- -- --                         

mariomeraz@raspberrypi: ~$   

Let’s start installing the OLED Display (There are two options) Although to make sure the installation of the OLED is performed depending on the brand of the OLED Device, we can issue both cli commands.

1.  Below is the first option to install the OLED from Adafruit

The OLED SSD1306 driver is based on the Adafruit GFX library which provides all the underlying graphics functions such as drawing pixels, lines, circles, etc. For more details about what you can do with the OLED check out the GFX library tutorial.

mariomeraz@raspberrypi: ~$  sudo pip3 install Adafruit-SSD1306 netifaces

Looking in indexes: https://pypi.org/simple, https://www.piwheels.org/simple

Collecting Adafruit-SSD1306

  Downloading https://www.piwheels.org/simple/adafruit-ssd1306/Adafruit_SSD1306-1.6.2-py3-none-any.whl

Collecting netifaces

  Downloading https://www.piwheels.org/simple/netifaces/netifaces-0.11.0-cp37-cp37m-linux_armv7l.whl

Collecting Adafruit-GPIO>=0.6.5 (from Adafruit-SSD1306)

  Downloading https://www.piwheels.org/simple/adafruit-gpio/Adafruit_GPIO-1.0.3-py3-none-any.whl

Collecting adafruit-pureio (from Adafruit-GPIO>=0.6.5->Adafruit-SSD1306)

  Downloading https://www.piwheels.org/simple/adafruit-pureio/Adafruit_PureIO-1.1.9-py3-none-any.whl

Requirement already satisfied: spidev in /usr/lib/python3/dist-packages (from Adafruit-GPIO>=0.6.5->Adafruit-SSD1306) (3.4)

Installing collected packages: adafruit-pureio, Adafruit-GPIO, Adafruit-SSD1306, netifaces

Successfully installed Adafruit-GPIO-1.0.3 Adafruit-SSD1306-1.6.2 adafruit-pureio-1.1.9 netifaces-0.11.0

mariomeraz@raspberrypi: ~$   

2.  Below is the second option

luma. oled provides a Python3 interface to OLED matrix displays with the SSD1306, SSD1309, SSD1322, SSD1325, SSD1327, SSD1331, SSD1351, SSD1362, SH1106 or WS0010 controllers to connect with Raspberry Pi and other Linux-based single-board computers.

mariomeraz@raspberrypi: ~$    pip3 install luma.oled

Looking in indexes: https://pypi.org/simple, https://www.piwheels.org/simple

Collecting luma.oled

  Downloading https://files.pythonhosted.org/packages/d5/3c/2a464be33c7a29633506b75c579cb50356a1e788609db809bf7999c74511/luma.oled-3.8.1-py2.py3-none-any.whl

Collecting luma.core>=2.0.0 (from luma.oled)

  Downloading https://files.pythonhosted.org/packages/e9/c8/878165a9413bcf4745a396809646f16a2eb00eba5589bf5aac1817bf3ce3/luma.core-2.3.1-py2.py3-none-any.whl (71kB)

    100% |\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588| 71kB 1.6MB/s 

Requirement already satisfied: RPI.GPIO; platform_system == "Linux" in /usr/lib/python3/dist-packages (from luma.core>=2.0.0->luma.oled) (0.7.0)

Collecting deprecated (from luma.core>=2.0.0->luma.oled)

  Downloading https://files.pythonhosted.org/packages/51/6a/c3a0408646408f7283b7bc550c30a32cc791181ec4618592eec13e066ce3/Deprecated-1.2.13-py2.py3-none-any.whl

Requirement already satisfied: pillow>=4.0.0 in /usr/lib/python3/dist-packages (from luma.core>=2.0.0->luma.oled) (5.4.1)

Collecting smbus2 (from luma.core>=2.0.0->luma.oled)

  Downloading https://files.pythonhosted.org/packages/71/2f/73aad66cdee8d4b94068bbc80164aa6a24b3f83541de7b04974438fd70e6/smbus2-0.4.2-py2.py3-none-any.whl

Collecting cbor2 (from luma.core>=2.0.0->luma.oled)

  Downloading https://www.piwheels.org/simple/cbor2/cbor2-5.4.3-cp37-cp37m-linux_armv7l.whl (99kB)

    100% |\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588| 102kB 256kB/s 

Requirement already satisfied: spidev; platform_system == "Linux" in /usr/lib/python3/dist-packages (from luma.core>=2.0.0->luma.oled) (3.4)

Collecting pyftdi (from luma.core>=2.0.0->luma.oled)

  Downloading https://files.pythonhosted.org/packages/17/ce/a97811c3e7e2d5a9520b88801dcc70ac1b553ed31b9819b2fce14ffa9aa3/pyftdi-0.54.0-py3-none-any.whl (144kB)

    100% |\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588| 153kB 1.3MB/s 

Requirement already satisfied: wrapt<2,>=1.10 in /usr/lib/python3/dist-packages (from deprecated->luma.core>=2.0.0->luma.oled) (1.10.11)

Collecting pyusb!=1.2.0,>=1.0.0 (from pyftdi->luma.core>=2.0.0->luma.oled)

  Downloading https://files.pythonhosted.org/packages/15/a8/4982498b2ab44d1fcd5c49f07ea3795eab01601dc143b009d333fcace3b9/pyusb-1.2.1-py3-none-any.whl (58kB)

    100% |\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588| 61kB 1.6MB/s 

Requirement already satisfied: pyserial>=3.0 in /usr/lib/python3/dist-packages (from pyftdi->luma.core>=2.0.0->luma.oled) (3.4)

Installing collected packages: deprecated, smbus2, cbor2, pyusb, pyftdi, luma.core, luma.oled

Successfully installed cbor2-5.4.3 deprecated-1.2.13 luma.core-2.3.1 luma.oled-3.8.1 pyftdi-0.54.0 pyusb-1.2.1 smbus2-0.4.2

## Project Python Script, The famous “Hello World!” plus your name

This code is available in git hub:

[https://github.com/mariomeraztechauthor/Linux_Raspberrypi_Book/blob/main/raspberry_python_hello_world](https://github.com/mariomeraztechauthor/Linux_Raspberrypi_Book/blob/main/raspberry_python_hello_world)

from luma.core.interface.serial import i2c

from luma.core.render import canvas

from luma.oled.device import sh1106

import time

serial = i2c(port=1, address=0x3C )

device = sh1106(serial)

with canvas(device) as draw:

        draw.rectangle(device.bounding_box, outline="white", fill="black")

        draw.text ((30, 15), "Hello World!", fill="white")

 draw.text ((30, 25), "Hola Mundo!", fill="white")

        draw.text ((30, 35), "Mario Meraz!", fill="white")

while True:

        time.sleep(1)

In the image below is the result of the python script

![A close-up of a circuit board Description automatically generated with low confidence](Images/image00302.jpeg)

## Project Monitoring your CPU

This code is available in git hub:

[https://github.com/mariomeraztechauthor/Linux_Raspberrypi_Book/blob/main/raspberry_python_CPU_Monitoring](https://github.com/mariomeraztechauthor/Linux_Raspberrypi_Book/blob/main/raspberry_python_CPU_Monitoring)

#! /usr/bin/env python3

#Python Imaging Library#

import Adafruit_SSD1306

import psutil

import netifaces as ni

from PIL import Image, ImageDraw, ImageFont

disp = Adafruit_SSD1306.SSD1306_128_64(rst=None)

disp.begin()

# Screen Configuration#

width = disp.width

height = disp.height

image = Image.new('1',(width,height))

draw = ImageDraw.Draw(image)

padding= -2

top = padding

bottom = height-padding

x= 0

# Measurements#

f = open ("/sys/class/thermal/thermal_zone0/temp","r")

t= f.readline()

t= float(t)

t= round(t/1000,1)

cpu= psutil.cpu_percent(interval=1)

cpu= round(cpu)

memory= psutil.virtual_memory()

memory= memory[1]

memory= round(memory /1024/ 1024)

if t> 50:

ALERT = "CPU TEMP ALERT"

else:

ALERT = "NOMINAL"

# Text in the Screen#

draw.text((x,top), "CPU Temp is: " +str(t)+"C",font=ImageFont.load_default(),fill=255)

draw.text((x,top+8), "CPU usage is: " +str(cpu)+"%",font=ImageFont.load_default(),fill=255)

draw.text((x, top+16), ALERT,font=ImageFont.load_default(),fill=255)

draw.text((x,top+25), str(memory)+ "MB Free",font=ImageFont.load_default(),fill=255)

draw.text ((x,top+ 35), "Mario Meraz", fill="white")

#Display values#

disp.image(image)

disp.display()

In the image below is the result of the python script

![](Images/image00303.jpeg)

| Table of connections between the hardware device Vs the Raspberry Pi |
| OLED | <CONNECTION> | Raspberry Pi |
| GND | to | [PIN 39] [GND] |
| VCC+ | to | [PIN 2] [5V] [POWER] |
| SCL | to | [PIN 5] [GPIO3] [SCL1] [I2C] |
| SDA | to | [PIN 3] [GPIO2] [SDA1][I2C] |
|  |  |  |

## Project Temperature Sensor

For this project we will use the Temperature sensors either the DHT22 or the DHT11.

![Graphical user interface Description automatically generated](Images/image00304.jpeg)

The DHT22 is the more expensive version which obviously has better specifications. Its temperature measuring range is from -40 to +125 degrees Celsius with +-0.5 degrees accuracy, while the DHT11 temperature range is from 0 to 50 degrees Celsius with +-2 degrees accuracy.

| Table of connections between the hardware device Vs the Raspberry Pi |
| DHT11/22 SENSOR | <CONNECTION> | Raspberry Pi |
| GND | to | [PIN 39] [GND] |
| VCC+ | to | [PIN 4] [5V] [POWER] |
| SIGNAL | to | [PIN 7] [GPIO4] [1-WIRE] |
|  |  |  |

Use the following wiring logic if you have a DHT11 or DHT22 sensor with and need to add a separate pull up resistor.

*   DHT11/22 Sensor Vcc+ to Raspberry Pi 5V
*   DHT11/22 Sensor GND to Raspberry Pi GND
*   DHT11/22 Sensor Signal to Raspberry Pi PIN 7 (GPIO PIN 4)
*   If the Sensor is Stand-Alone (No module) It will be needed a 10K Ohm Resistor between DHT11/22 PIN 1 and PIN 2

There are sensors that have a module and these ones already have a 10K-Ohms Resistor included in the module. If you wired everything up correctly, you’ll see a red LED glowing on the DHT11 module.  (NOTE: Some cost reduced modules do not include this LED.) Once that the Sensor is connected and cable out, if everything is ok, we should see a red led light. Next thing we need to do is install the DHT python library. This is done by entering  the following command:

mariomeraz@raspberrypi: ~$   sudo pip3 install Adafruit_DHT

Looking in indexes: https://pypi.org/simple, https://www.piwheels.org/simple

Requirement already satisfied: Adafruit_DHT in /usr/local/lib/python3.7/dist-packages/Adafruit_DHT-1.4.0-py3.7-linux-armv7l.egg (1.4.0)

mariomeraz@raspberrypi: ~$   

Note: If you run into problems with the above command, you may not have PIP installed on your Pi.  You can fix that by running the following commands.  These will install PIP and other utilities you may need.

 mariomeraz@raspberrypi: ~$   sudo apt-get install python3-dev python3-pip

Reading package lists... Done

Building dependency tree       

Reading state information... Done

python3-dev is already the newest version (3.7.3-1).

python3-dev set to manually installed.

python3-pip is already the newest version (18.1-5+rpt1).

The following packages were automatically installed and are no longer required:

  libmicrodns0 rpi-eeprom-images

Use 'sudo apt autoremove' to remove them.

0 upgraded, 0 newly installed, 0 to remove and 226 not upgraded.

 mariomeraz@raspberrypi: ~$

 mariomeraz@raspberrypi: ~$  sudo python3 -m pip install --upgrade pip setuptools wheel

Looking in indexes: https://pypi.org/simple, https://www.piwheels.org/simple

Collecting pip

  Downloading https://files.pythonhosted.org/packages/09/bd/2410905c76ee14c62baf69e3f4aa780226c1bbfc9485731ad018e35b0cb5/pip-22.3.1-py3-none-any.whl (2.1MB)

    100% |\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588| 2.1MB 131kB/s 

Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ProtocolError('Connection aborted.', RemoteDisconnected('Remote end closed connection without response'))': /simple/setuptools/

Collecting setuptools

  Downloading https://files.pythonhosted.org/packages/b6/40/353c051f77ee5618adaf1fd96f4f6bae9714ed0a22c7142c01c24eb77fe4/setuptools-65.5.1-py3-none-any.whl (1.2MB)

    100% |\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588\u2588| 1.2MB 213kB/s 

Collecting wheel

  Downloading https://files.pythonhosted.org/packages/3b/48/7a4e6e610cfbc71d727ac58ddc9abe0daf5772b81d5630a4aef9e919ad46/wheel-0.38.3-py3-none-any.whl

Installing collected packages: pip, setuptools, wheel

  Found existing installation: pip 18.1

    Not uninstalling pip at /usr/lib/python3/dist-packages, outside environment /usr

    Can't uninstall 'pip'. No files were found to uninstall.

  Found existing installation: setuptools 40.8.0

    Not uninstalling setuptools at /usr/lib/python3/dist-packages, outside environment /usr

    Can't uninstall 'setuptools'. No files were found to uninstall.

  Found existing installation: wheel 0.32.3

    Not uninstalling wheel at /usr/lib/python3/dist-packages, outside environment /usr

    Can't uninstall 'wheel'. No files were found to uninstall.

Successfully installed pip-22.3.1 setuptools-65.5.1 wheel-0.38.3

mariomeraz@raspberrypi: ~$

Let’s take a look at the code we are going to use. The first section of code imports the DHT library from Adafruit and the system time library.

import Adafruit_DHT

import time

This line defines the sensor object we will use, and the next line is a variable that defines the GPIO pin we are using.

DHT_SENSOR = Adafruit_DHT.DHT11

DHT_PIN = 4

Finally, the code loop that goes next.  The “while True:” line will force everything indented after running in an infinite loop. First, we capture the temperature and humidity to two aptly named variables,  and then use an IF statement to check to see if it worked. If it worked, we print the temperature and humidity to the screen. If it failed, we let you know to check your wiring.

![A picture containing electronics, connector Description automatically generated](Images/image00305.jpeg)

Python Code Sensor DHT

This code is available in git hub:

[https://github.com/mariomeraztechauthor/Linux_Raspberrypi_Book/blob/main/raspberry_python_DHT11_22Sensor](https://github.com/mariomeraztechauthor/Linux_Raspberrypi_Book/blob/main/raspberry_python_DHT11_22Sensor)

import Adafruit_DHT

import time

DHT_SENSOR = Adafruit_DHT.DHT11

DHT_PIN = 4   # GPIO PIN That is in used #

#measurements #

while True:

humidity, temperature = Adafruit_DHT.read(DHT_SENSOR, DHT_PIN)

if humidity is not None and temperature is not None:

print("Temp= {0:0.1f}C Humidity={1:0.1f}%".format(temperature,humidity))

else:

print("Sensor failure. Check the wiring");

time.sleep(3);

Outcome from Sensor DHT11/22

Python 3.7.3 (/usr/bin/python3)

>>> %Run sensorDHT.py

Temp= 22.0C Humidity=75.0%

Temp= 22.0C Humidity=76.0%

Temp= 22.0C Humidity=84.0%

Temp= 24.0C Humidity=77.0%

Temp= 24.0C Humidity=73.0%

# Output with  wiring issues #

Sensor failure. Check the wiring

Sensor failure. Check the wiring

Reference:

[https://www.thegeekpub.com/236867/using-the-dht11-temperature-sensor-with-the-raspberry-pi/](https://www.thegeekpub.com/236867/using-the-dht11-temperature-sensor-with-the-raspberry-pi/)

## Project BMP180 Sensor (Pressure, Temperature and Altitude) .

The BMP180 Digital pressure sensor can detect pressure, temperature, and altitude. We will use the Raspberry pi in this project to input this data from the BMP180 sensor through the I2C interface.

First, make sure the I2C Interface is enabled

Click on the Raspberry Symbol -> ![](Images/image00287.jpeg)Then Go to Preferences -> Then Go to Raspberry Pi Configuration and then select the Interfaces tab to enable the I2C, therefore you will see the screen below

![Graphical user interface, table Description automatically generated](Images/image00299.jpeg)

To start- off it is needed to install some libraries for Python to know how to read the output of the BMP180.

Adafruit uses the libraries that were written for the predecessor model of the BMP180 which is the BMP085, this is doable since the chips were designed to be compatible with each other therefore the libraries work for BMP180.

![](Images/image00306.jpeg)![Graphical user interface, application Description automatically generated](Images/image00307.jpeg)![Graphical user interface Description automatically generated](Images/image00308.jpeg)

Step 1.  Git Installation

Install the GIT application since this will be used to retrieve the code from GitHub

mariomeraz@raspberrypi: ~$ sudo apt-get update

Get:1 https://download.docker.com/linux/raspbian buster InRelease [33.6 kB]

Get:2 http://archive.raspberrypi.org/debian buster InRelease [32.6 kB]         

Get:3 http://raspbian.raspberrypi.org/raspbian buster InRelease [15.0 kB]      

Get:4 https://download.docker.com/linux/raspbian buster/stable armhf Packages [23.1 kB]

Get:5 http://archive.raspberrypi.org/debian buster/main armhf Packages [392 kB]

Get:6 http://raspbian.raspberrypi.org/raspbian buster/main armhf Packages [13.0 MB]

Fetched 13.5 MB in 53s (256 kB/s)                                              

Reading package lists... Done

mariomeraz@raspberrypi: ~$  

mariomeraz@raspberrypi: ~$ sudo apt-get install git build-essential

Reading package lists... Done

Building dependency tree       

Reading state information... Done

build-essential is already the newest version (12.6).

The following packages were automatically installed and are no longer required:

  libmicrodns0 rpi-eeprom-images

Use 'sudo apt autoremove' to remove them.

Suggested packages:

  git-daemon-run | git-daemon-sysvinit git-doc git-el git-email git-gui gitk

  gitweb git-cvs git-mediawiki git-svn

The following packages will be upgraded:

  git

1 upgraded, 0 newly installed, 0 to remove and 251 not upgraded.

Need to get 4,195 kB of archives.

After this operation, 4,096 B of additional disk space will be used.

Do you want to continue? [Y/n] y

Get:1 http://mirror.fcix.net/raspbian/raspbian buster/main armhf git armhf 1:2.20.1-2+deb10u4 [4,195 kB]

Fetched 4,195 kB in 2s (2,709 kB/s)

Reading changelogs... Done

(Reading database ... 101183 files and directories currently installed.)

Preparing to unpack .../git_1%3a2.20.1-2+deb10u4_armhf.deb ...

Unpacking git (1:2.20.1-2+deb10u4) over (1:2.20.1-2+deb10u3) ...

Setting up git (1:2.20.1-2+deb10u4) ...

mariomeraz@raspberrypi: ~$  

mariomeraz@raspberrypi: ~$  sudo apt-get install python-smbus

Reading package lists... Done

Building dependency tree       

Reading state information... Done

python-smbus is already the newest version (4.1-1).

The following packages were automatically installed and are no longer required:

  libmicrodns0 rpi-eeprom-images

Use 'sudo apt autoremove' to remove them.

0 upgraded, 0 newly installed, 0 to remove and 251 not upgraded.

mariomeraz@raspberrypi: ~$   

Step 2\. Directory creation. We will use the name BMP180_Code

mariomeraz@raspberrypi: ~$  mkdir ~/BMP180_Code

mariomeraz@raspberrypi: ~$  cd ~/BMP180_Code

mariomeraz@raspberrypi:  ~/BMP180_Code $ 

Step 3\. Git Repository download for the BMP180\.

This instruction below will download the contents of the Adafruit Python library to the current location:

Git clone [https://github.com/adafruit/Adafruit_Python_BMP.git](https://github.com/adafruit/Adafruit_Python_BMP.git)

This library will need to be compiled; therefore, the instructions below are needed:

mariomeraz@raspberrypi: ~$  cd Adafruit_Python_BMP

mariomeraz@raspberrypi: ~$ sudo python setup.py install

mariomeraz@raspberrypi: ~/BMP180_Code $ git clone https://github.com/adafruit/Adafruit_Python_BMP.git

Cloning into 'Adafruit_Python_BMP'...

remote: Enumerating objects: 82, done.

remote: Total 82 (delta 0), reused 0 (delta 0), pack-reused 82

Unpacking objects: 100% (82/82), done.

mariomeraz@raspberrypi:  ~/BMP180_Code $ 

mariomeraz@raspberrypi:  ~/BMP180_Code $ cd Adafruit_Python_BMP

mariomeraz@raspberrypi:  ~/BMP180_Code/Adafruit_Python_BMP $ sudo python setup.py install

running install

running bdist_egg

running egg_info

creating Adafruit_BMP.egg-info

writing requirements to Adafruit_BMP.egg-info/requires.txt

writing Adafruit_BMP.egg-info/PKG-INFO

writing top-level names to Adafruit_BMP.egg-info/top_level.txt

writing dependency_links to Adafruit_BMP.egg-info/dependency_links.txt

writing manifest file 'Adafruit_BMP.egg-info/SOURCES.txt'

reading manifest file 'Adafruit_BMP.egg-info/SOURCES.txt'

writing manifest file 'Adafruit_BMP.egg-info/SOURCES.txt'

installing library code to build/bdist.linux-armv7l/egg

running install_lib

running build_py

creating build

creating build/lib.linux-armv7l-2.7

creating build/lib.linux-armv7l-2.7/Adafruit_BMP

copying Adafruit_BMP/BMP085.py -> build/lib.linux-armv7l-2.7/Adafruit_BMP

copying Adafruit_BMP/__init__.py -> build/lib.linux-armv7l-2.7/Adafruit_BMP

creating build/bdist.linux-armv7l

creating build/bdist.linux-armv7l/egg

creating build/bdist.linux-armv7l/egg/Adafruit_BMP

copying build/lib.linux-armv7l-2.7/Adafruit_BMP/BMP085.py -> build/bdist.linux-armv7l/egg/Adafruit_BMP

copying build/lib.linux-armv7l-2.7/Adafruit_BMP/__init__.py -> build/bdist.linux-armv7l/egg/Adafruit_BMP

byte-compiling build/bdist.linux-armv7l/egg/Adafruit_BMP/BMP085.py to BMP085.pyc

byte-compiling build/bdist.linux-armv7l/egg/Adafruit_BMP/__init__.py to __init__.pyc

creating build/bdist.linux-armv7l/egg/EGG-INFO

copying Adafruit_BMP.egg-info/PKG-INFO -> build/bdist.linux-armv7l/egg/EGG-INFO

copying Adafruit_BMP.egg-info/SOURCES.txt -> build/bdist.linux-armv7l/egg/EGG-INFO

copying Adafruit_BMP.egg-info/dependency_links.txt -> build/bdist.linux-armv7l/egg/EGG-INFO

copying Adafruit_BMP.egg-info/requires.txt -> build/bdist.linux-armv7l/egg/EGG-INFO

copying Adafruit_BMP.egg-info/top_level.txt -> build/bdist.linux-armv7l/egg/EGG-INFO

zip_safe flag not set; analyzing archive contents...

creating dist

creating 'dist/Adafruit_BMP-1.5.4-py2.7.egg' and adding 'build/bdist.linux-armv7l/egg' to it

removing 'build/bdist.linux-armv7l/egg' (and everything under it)

Processing Adafruit_BMP-1.5.4-py2.7.egg

Copying Adafruit_BMP-1.5.4-py2.7.egg to /usr/local/lib/python2.7/dist-packages

Adding Adafruit-BMP 1.5.4 to easy-install.pth file

mariomeraz@raspberrypi:  ~/BMP180_Code/Adafruit_Python_BMP $ 

mariomeraz@raspberrypi:  ~/BMP180_Code/Adafruit_Python_BMP $ sudo apt-get install python-smbus i2c-tools

Reading package lists... Done

Building dependency tree       

Reading state information... Done

i2c-tools is already the newest version (4.1-1).

i2c-tools set to manually installed.

python-smbus is already the newest version (4.1-1).

The following packages were automatically installed and are no longer required:

  libmicrodns0 rpi-eeprom-images

Use 'sudo apt autoremove' to remove them.

0 upgraded, 0 newly installed, 0 to remove and 251 not upgraded.

mariomeraz@raspberrypi:  ~/BMP180_Code/Adafruit_Python_BMP $ 

mariomeraz@raspberrypi:  ~/BMP180_Code/Adafruit_Python_BMP $ sudo apt-get install build-essential python-dev python-smbus

Reading package lists... Done

Building dependency tree       

Reading state information... Done

build-essential is already the newest version (12.6).

python-dev is already the newest version (2.7.16-1).

python-smbus is already the newest version (4.1-1).

The following packages were automatically installed and are no longer required:

  libmicrodns0 rpi-eeprom-images

Use 'sudo apt autoremove' to remove them.

0 upgraded, 0 newly installed, 0 to remove and 251 not upgraded.

mariomeraz@raspberrypi: ~/BMP180_Code/Adafruit_Python_BMP $ 

mariomeraz@raspberrypi:  ~/BMP180_Code/Adafruit_Python_BMP $ git clone https://github.com/sunfounder/Adafruit_Python_BMP.git

Cloning into 'Adafruit_Python_BMP'...

remote: Enumerating objects: 44, done.

remote: Total 44 (delta 0), reused 0 (delta 0), pack-reused 44

Unpacking objects: 100% (44/44), done.

mariomeraz@raspberrypi:  ~/BMP180_Code/Adafruit_Python_BMP $ 

mariomeraz@raspberrypi: ~$ sudo apt-get install python-dev python-rpi.gpio

Reading package lists... Done

Building dependency tree       

Reading state information... Done

python-dev is already the newest version (2.7.16-1).

The following packages were automatically installed and are no longer required:

  libmicrodns0 rpi-eeprom-images

Use 'sudo apt autoremove' to remove them.

The following NEW packages will be installed:

  rpi.gpio-common

The following packages will be upgraded:

  python-rpi.gpio

1 upgraded, 1 newly installed, 0 to remove and 250 not upgraded.

Need to get 26.7 kB of archives.

After this operation, 14.3 kB of additional disk space will be used.

Get:1 http://archive.raspberrypi.org/debian buster/main armhf rpi.gpio-common armhf 0.7.0-0.1~bpo10+4 [5,952 B]

Get:2 http://archive.raspberrypi.org/debian buster/main armhf python-rpi.gpio armhf 0.7.0-0.1~bpo10+4 [20.7 kB]

Fetched 26.7 kB in 1s (43.4 kB/s)          

Reading changelogs... Done

Selecting previously unselected package rpi.gpio-common:armhf.

(Reading database ... 101183 files and directories currently installed.)

Preparing to unpack .../rpi.gpio-common_0.7.0-0.1~bpo10+4_armhf.deb ...

Unpacking rpi.gpio-common:armhf (0.7.0-0.1~bpo10+4) ...

Preparing to unpack .../python-rpi.gpio_0.7.0-0.1~bpo10+4_armhf.deb ...

Unpacking python-rpi.gpio (0.7.0-0.1~bpo10+4) over (0.7.0~buster-1) ...

Setting up rpi.gpio-common:armhf (0.7.0-0.1~bpo10+4) ...

Setting up python-rpi.gpio (0.7.0-0.1~bpo10+4) ...

mariomeraz@raspberrypi: ~$  

Step 4\. Table of connections

| Table of connections between the hardware device Vs the Raspberry Pi |
| BMP180 | <CONNECTION> | Raspberry Pi |
| GND | to | [PIN 34] [GND] |
| VCC+  | to | [PIN 17] [3.3 V] [POWER] |
| SCL | to | [PIN 5] [GPIO3] [SCL1] [I2C] |
| SDA | to | [PIN 3] [GPIO2] [SDA1][I2C] |
|  |  |  |

Step 5\. Python Code for BMP180 with the compatibility information of the BMP085

This code is available in git hub:

[https://github.com/mariomeraztechauthor/Linux_Raspberrypi_Book/blob/main/raspberry_python_BMP180_085](https://github.com/mariomeraztechauthor/Linux_Raspberrypi_Book/blob/main/raspberry_python_BMP180_085)

#!/usr/bin/python

import Adafruit_BMP.BMP085 as BMP085 #  BMP library

sensor = BMP085.BMP085()

print 'Temp = {0:0.2f} *C'.format(sensor.read_temperature()) # Temperature 

print 'Pressure = {0:0.2f} Pa'.format(sensor.read_pressure()) # pressure

print 'Altitude = {0:0.2f} m'.format(sensor.read_altitude()) #  altitude

Outcome from the python script:

>>> %Run sensorBMP180.py

Temperature: 23.50 C

Pressure:    1009.03 hPa

Altitude:    43.27

## Projects with the Raspberry Pi Camera

The Raspberry Pi Camera V2 features an 8-megapixel Sony IMX219 image sensor with fixed focus lens, it is capable of 3280×2464-pixel static images and supports 1080p30, 720p60, and 640×480p90 video. The camera is compatible with all Raspberry Pi boards, but if you want to use it with the Pi Zero, you need an adapter cable.

![A picture containing text, electronics Description automatically generated](Images/image00309.jpeg)![A picture containing electronics Description automatically generated](Images/image00310.jpeg)

![A picture containing items, electronic, automaton Description automatically generated](Images/image00311.jpeg)

Please make sure to enable the Pi Camera with the instructions below:

Click on the Raspberry Symbol -> ![](Images/image00287.jpeg)Then Go to Preferences -> Then Go to Raspberry Pi Configuration and then select the Interfaces tab to enable the Camera, therefore you will see the screen below

![Graphical user interface, table Description automatically generated](Images/image00299.jpeg)

mariomeraz@raspberrypi:  ~ $ sudo apt-get install python-picamera

Reading package lists... Done

Building dependency tree       

Reading state information... Done

python-picamera is already the newest version (1.13).

The following packages were automatically installed and are no longer required:

  libmicrodns0 rpi-eeprom-images

Use 'sudo apt autoremove' to remove them.

0 upgraded, 0 newly installed, 0 to remove and 250 not upgraded.

mariomeraz@raspberrypi:  ~ $ 

mariomeraz@raspberrypi:  ~ $ sudo apt-get update

Hit:1 https://download.docker.com/linux/raspbian buster InRelease

Get:2 http://archive.raspberrypi.org/debian buster InRelease [32.6 kB]         

Get:3 http://raspbian.raspberrypi.org/raspbian buster InRelease [15.0 kB]      

Get:4 http://raspbian.raspberrypi.org/raspbian buster/main armhf Packages [13.0 MB]

Get:5 http://archive.raspberrypi.org/debian buster/main armhf Packages [392 kB]

Fetched 13.5 MB in 18s (750 kB/s)                                              

Reading package lists... Done

mariomeraz@raspberrypi:  ~ $ 

mariomeraz@raspberrypi:  ~ $ sudo apt-get upgrade

Reading package lists... Done

Building dependency tree       

Reading state information... Done

Calculating upgrade... Done

The following packages were automatically installed and are no longer required:

  libmicrodns0 python-colorzero rpi-eeprom-images

Use 'sudo apt autoremove' to remove them.

The following packages have been kept back:

  raspberrypi-sys-mods raspberrypi-ui-mods

The following packages will be upgraded:

  aspell base-files bind9-host bluez bzip2 chromium-browser

  chromium-browser-l10n chromium-codecs-ffmpeg-extra cifs-utils containerd.io

  curl dbus dbus-user-session dbus-x11 debconf debconf-i18n debconf-utils

  dillo distro-info-data docker-ce docker-ce-cli dpkg dpkg-dev ffmpeg

  firmware-atheros firmware-brcm80211 firmware-libertas firmware-misc-nonfree

  firmware-realtek git-man golang-docker-credential-helpers gpicview

  gstreamer1.0-plugins-good gzip isc-dhcp-client isc-dhcp-common klibc-utils

  libasound2 libasound2-data libaspell15 libatk-wrapper-java

  libatk-wrapper-java-jni libavcodec58 libavdevice58 libavfilter7

  libavformat58 libavresample4 libavutil56 libbind9-161 libbluetooth3

  libbluray2 libbz2-1.0 libc-bin libc-dev-bin libc-l10n libc6 libc6-dbg

  libc6-dev libcairo-gobject2 libcairo2 libcups2 libc

mariomeraz@raspberrypi:  ~ $ pip install picamera

Defaulting to user installation because normal site-packages is not writeable

Looking in indexes: https://pypi.org/simple, https://www.piwheels.org/simple

Requirement already satisfied: picamera in /usr/lib/python3/dist-packages (1.13)

mariomeraz@raspberrypi:  ~ $ 

Python Code for Pi Camera Preview

This code is available in git hub:

[https://github.com/mariomeraztechauthor/Linux_Raspberrypi_Book/blob/main/raspberry_python_picamera](https://github.com/mariomeraztechauthor/Linux_Raspberrypi_Book/blob/main/raspberry_python_picamera)

#!/usr/bin/python

from picamera import PiCamera

from time import sleep

camera = PiCamera()

camera.start_preview()

sleep(5)

camera.stop_preview()

Output after successfully process the code:

>>> %Run camerapreview.py

>>> %Run camerapreview.py

>>> %Run camerapreview.

Python code to take pictures

#!/usr/bin/python

from picamera import PiCamera

from time import sleep

camera = PiCamera()

camera.start_preview()

for i in range(5):

    sleep(5)

    camera.capture('/home/pi/Desktop/image%s.jpg' % i)

    camera.stop_preview()

Output after successfully process the code:

>>> %Run pi_camera.py

>>> 

Other cli instructions for the pi camera to take pictures

mariomeraz@raspberrypi:  ~ $ cd Desktop

mariomeraz@raspberrypi:  ~/Desktop $ mkdir photo

The following instruction takes a photo

mariomeraz@raspberrypi:  ~/Desktop/photo $  raspistill -o image.jpg

mariomeraz@raspberrypi:  ~/Desktop/photo $ 

The imagen taken is below:

![A picture containing wall, indoor, person Description automatically generated](Images/image00312.jpeg)

Video. What is H.264 ?

H. 264 is a well-known video compression standard for high-definition digital video. Also known as MPEG-4 Part 10 or Advanced Video Coding (MPEG-4 AVC), H. 264 is defined as a block-oriented, compensation-based video compression standard that defines multiple profiles (tools) and levels (max bitrates and resolutions). MP4 is a file container format, while H. 264 is a video compression codec that requires a video container to host the encoded video.

The instruction below takes the video in H.264 compression codec

mariomeraz@raspberrypi: ~$   raspivid -o movie.h264 -t 5000

Video taken with the raspberry pi camera

![A person holding a cell phone Description automatically generated with low confidence](Images/image00313.jpeg)

## Fundamental Projects to build your Stack of Knowledge.

The following projects are foundational in order to expand the capabilities of what can be done with a Raspberry pi and the utilities on it.

Step 1\. Node. Js Installation

The package for the Node.Js is Node Package Manager (npm)

mariomeraz@raspberrypi: ~$  sudo wget http://nodejs.org/dist/v0.10.21/node-v0.10.21-linux-arm-pi.tar.gz

Step 2\. Node Package Extraction

mariomeraz@raspberrypi: ~$  sudo tar -xvzf node-v0.10.21-linux-arm-pi.tar.gz

Step 3\. Symbolic links for Node and npm binaries creation.

mariomeraz@raspberrypi: ~$  sudo ln-s /var/www/node-v0.10.21-linux-arm-pi/bin/node /bin/node

mariomeraz@raspberrypi: ~$  sudo ln-s /var/www/node-v0.10.21-linux-arm-pi/bin/npm /bin/npm

Extra Modules

mariomeraz@raspberrypi: ~$  npm install socket.io node-static socket.io adafrui-i2c-pwm-driver sleep optimist

Docker Installation

mariomeraz@raspberrypi: ~$     curl -ssl get.docker.com | sh

mariomeraz@raspberrypi: ~$     sudo usermod pi -aG docker

GitHub clone repository

mariomeraz@raspberrypi: ~$  apt-get update && apt-get -any install git jq

mariomeraz@raspberrypi: ~$  sudo apt update

Get:1 https://download.docker.com/linux/raspbian buster InRelease [33.6 kB]

Get:2 http://archive.raspberrypi.org/debian buster InRelease [32.6 kB]         

Get:3 http://raspbian.raspberrypi.org/raspbian buster InRelease [15.0 kB]      

Get:4 https://download.docker.com/linux/raspbian buster/stable armhf Packages [21.1 kB]

Get:5 http://raspbian.raspberrypi.org/raspbian buster/main armhf Packages [13.0 MB]

Get:6 http://archive.raspberrypi.org/debian buster/main armhf Packages [392 kB]

Get:7 http://raspbian.raspberrypi.org/raspbian buster/contrib armhf Packages [58.8 kB]

Get:8 http://raspbian.raspberrypi.org/raspbian buster/non-free armhf Packages [104 kB]

Fetched 13.7 MB in 49s (281 kB/s)                                              

Reading package lists... Done

Building dependency tree       

Reading state information... Done

224 packages can be upgraded. Run 'apt list --upgradable' to see them.

N: Repository 'http://raspbian.raspberrypi.org/raspbian buster InRelease' changed its 'Suite' value from 'stable' to 'oldstable'

N: Repository 'http://archive.raspberrypi.org/debian buster InRelease' changed its 'Suite' value from 'testing' to 'oldstable'

mariomeraz@raspberrypi: ~$   

Web interface to control a Raspberry Pi

*   Fileserver
*   Media Center
*   Remote Control via Web

Requirements

*   Raspberry pi
*   RaspCTL

Step 1\. Update the Raspberry Pi

Raspberry Pi Operating System Update

mariomeraz@raspberrypi: ~$  sudo apt-get update && apt-get upgrade

Firmware Update

mariomeraz@raspberrypi: ~$  sudo rip-update

Booting to LXDE

mariomeraz@raspberrypi: ~$  raspi-config

Step 2\. Edit the IP

The raspberry pi needs a static IP

Networking Config update

mariomeraz@raspberrypi: ~$  sudo nano /etc/network/interfaces

Change iface eth0 inet dhcp to iface eth0 inet static

Step 3\. Set up a static IP

The following lines need to be added under the iface line:

Address 192.168.1.[IP]

Net ask 255.255.255.0

Network 192.168.1.0

Broadcast 192.168.1.255

Gateway 192.168.1.[Router IP]

Step. 4 RaspCTL Installation

Public Keys from RaspCTL are needed

mariomeraz@raspberrypi: ~$  wget debrepo.kernel.org/raspctl.asc

mariomeraz@raspberrypi: ~$  cat raspctl.asc | sudo apt-key add -

Step 5\. Add Repository & Install

Add the repository to the source’s file with the following cli command:

mariomeraz@raspberrypi: ~$   echo “deb http://debrepo.kernel.org/ raspctl main” |

mariomeraz@raspberrypi: ~$  sudo tee/etc/apt/sources.list.d/raspctl.list

Software Installation

mariomeraz@raspberrypi: ~$   sudo apt-get update

mariomeraz@raspberrypi: ~$   sudo apt-get install raspctl

Step 6\. Access the Raspberry Pi

To start the access to the raspberry pi

 [Http://[IP]:8086](Http://%5BIP%5D:8086)

## Project Twilio: Send an SMS from the Raspberry Pi

![Graphical user interface, text, application, email Description automatically generated](Images/image00314.jpeg)

This is a program that combines Twilio and Python to send a SMS (Short Message Service) from the Raspberry Pi to a Mobile phone.

Twilio is a cloud communication company, enables to send SMS messages for free from the Raspberry Pi to a Mobile phone using python code.

Step 1 . Set Up the Twilio Account

Twilio.com/try-Twilio

A) Twilio Registration

B) Twilio Account

C) Twilio Number

Twilio is free and enables the user to send an SMS to a registered and verified phone number.

Step 2\. Number Registration

*   There are two types of Twilio accounts, paid accounts, and free trail accounts

*   The number needs to be a verified number

*   The country code will need to be provided

Step 3\. The Dashboard

*   Once registered and logged in on Twilio.

*   AccountSid and the Auth Token will be available

*   These parameters are needed for the Twilio REST.

Step 4\. Twilio Software Installation

mariomeraz@raspberrypi: ~$   sudo easy_install twilio

mariomeraz@raspberrypi: ~$   sudo pip install twilio

In case “pip” is needed to be installed

mariomeraz@raspberrypi: ~$   sudo apt-get install python-pip python-dev

mariomeraz@raspberrypi: ~$   sudo pip install -U pip

Step 5\. Twilio Authentication

To create an SMS program that will send text messages to a mobile phone number.

In the python editor it is needed to import the Twilio REST libraries

*   Add the Account and credentials
*   AccountSid
*   Auth Token

from twilio.rest import twilioRestClient

Account_sid = “ XX”

#Enter the numbers

Auth_taken = “ XX “

Client = TwilioRestClient(account_sid, auth_token)

Step 6\. Create a message

This message will be sent to the mobile phone number

message = raw_input (“Please enter the message” )

Step 7\. Add a number

To send the message are needed two numbers.

The first number is the mobile phone number.

The second number below is the Twilio Account number that can be retrieved from the dashboard page under “Call the sandbox number”

message = client.message.create (to= “+1-TheMobileNumber”,

from_=“+1-TWILIONumber”, body=message)

Step 8\. Send a message

This message below it is just a confirmation message

print message.Sid

print “ The message has been sent”

Complete Code in Python:

from twilio.rest from TwilioRestClient Account_sid = “ XX”

#Enter the phone numbers#

Auth_taken = “ XX “

Client = TwilioRestClient(account_sid, auth_token)

message = raw_input (“Please enter the message” )

message = client.message.create (to= “+1-TheMobileNumber”,

from_=“+1-TWILIONumber”, body=message)

print message.Sid

print “ The message has been sent”

Alternative Python Code to send SMS

An additional way to send email messages and SMS with just python is the following way:

import smtplib

from email.message import EmailMessage

def email_alert (subject, body, to):

    msg = EmailMessage ()

    msg.set_content (body)

    msg [‘subject’] = subject

    msg [‘to’]  = to

    User = “[email_alert@gmail.com](mailto:email_alert@gmail.com) “

    msg [‘from’] = user

password = “pass”

server = smtplib.SMTP (“ smtp.gmail.com”

, 587)

sever.starttls ()

server.login( user, password)

server.send_message(msg)

sever.quit ()

if _name_  == ‘_main_’ :

  Email_alert(“ Hey”, Hello World,  “ email [alert@gmail.com](mailto:alert@gmail.com)“ )

  Email_alert(“ Hey”, Hello World,  “ number @carrier.com“ )  # SMS Delivery#

To set up a gmail account

Https:// myaccount.google.com

To send sms alerts:

Digitaltrends.com/mobile

Conclusion

That’s it, I hope you have learned new skills, but the most important thing is you enjoyed the process of learning.

THANK YOU! Mario Meraz