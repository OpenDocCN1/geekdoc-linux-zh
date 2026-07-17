![](Images/cover00905.jpeg)

![](Images/image00459.jpeg)

Copyright

First published on Amazon.com by Morgan Partridge in 2022

This edition was published in 2022 by Morgan Partridge

Copyright © 2022 Morgan Partridge

The moral right of the author has been asserted.

All rights reserved.

No part of this publication may be reproduced, stored in a retrieval system, or transmitted in any form or by any means, without the prior permission in writing of the author, nor otherwise circulated in any form of binding or cover other than that in which it is published and without a similar condition including this condition being imposed on the subsequent purchaser.

Disclaimer

All information in this book is provided on the “as is” basis without any warranty. However effort has been taken without exception while preparing this book, neither the author nor the publisher shall have any liability to any person or entity with respect to any loss of damage caused or alleged to be caused directly or indirectly by the contents of this book.

None of the content within this book is official or sponsored and is not supported by any trademark owners, whether open or closed source.

This book is only for self-help and learning purpose of customers.

Trademark

Trademarked names show up in this book, for example Blizzard Battle.net, Microsoft, Youtube and several more, and have been used in this book without intention of trademark infringement, and have been obscured with only the names used in an self-help or learning purpose and to the benefit of the trademark owner.

All trademarks are acknowledged as belonging to their respective owners.

This book is only for self-help and learning purpose of purchasers.

None of the content within this book is official or sponsored and is not supported by any trademark owners, whether open or closed source.

Linux is the registered trademark of Linux Torvalds in the U.S. and other countries.

Acknowledgements

To my family without whom none of this would have been possible.

Linus Torvalds is the creator of Linux and holder of the Linux trademark and is acknowledged as such, and he does not support or sponsor this self-help learning book.

Linux® is the registered trademark of Linus Torvalds in the U.S. and other countries

Linux Mark Institute and the community, for developing and maintaining Linux Mint 21 ‘Vanessa’.

Blizzard for developing and publishing World of Warcraft that I really love and enjoy.

WINE or Wine Is Not An Emulator for the compatibility layer.

Lutris making it far more accessible to Install and play games and software.

Gabe Newell and Valve for developing and publishing the Steam Store.

Install Machine Details

All details of this self help learning guide has been undertaken on bare metal or directly on hardware, rather than a virtual machine

The Install of Linux Mint 21 ‘Vanessa’ has been done on a manually partitioned drive with:

1 GB for the EFI partition

92 GB for the / or root partition

35 GB for the swap partition

The specifications of the computer used to Install Linux Mint 21 ‘Vanessa’ are:

CPU: Intel(R)Core(TM) i3-9100F CPU

RAM or Memory: 16GB DDR4

Motherboard: MSI B365M PRO-VH REV 1.0

GPU or Graphics Card: Gigabyte Nvidia 3060 GTX 12GB

Monitor: 21" Acer Monitor

SSD: 1618 GB Over Samsung, PNY and SPCC Drives

HDD Internal: 9TB over 2 Western Digital Drives

HDD External: 1TB JMicron

Soundcard: USB 3.0 External Phoinkas Soundcard

Speakers: Amazon Basics 2.0 Speakers

Headphones: Generic 2.0 Earphones

Headset: Kingston HyperX Cloud Alpha 3.5 MM

Keyboard 1 & 2: USB 2.0 Generic Mini Gaming Keyboard, USB 2.0 Basic Full Sized Keyboard

Mouse: USB 2.0 Trust Wireless Mouse X200, USB 2.0 Basic Wired Mouse

Network: Realtek Motherboard Gigabit PCI Port, USB 3.0 Realtek Gigabit Adapter

Phone: Samsung Smartphone

USB Hub: USB 3.0 External Phoinkas Soundcard

Printer: Epson Network Printer

Introduction

This guide was written to be an After Install Self Help Guide for Linux Mint 21 ‘Vanessa’.

To increase your security you will be required to ENTER your password to complete most steps on this list so be sure to have it at hand.

After typing in all sudo commands and your password you may be required to confirm by pressing ENTER to continue or ESC to abort.

Make sure you update and upgrade your Linux Mint 21 ‘Vanessa’ every day, a few days or as you like to ensure security and stability.

Do not ever use sudo apt auto remove as it could destabilize or break Linux Mint 21 ‘Vanessa’

You should type in what is stated to help you to remember but you can copy and paste if you wish.

Make sure to click Keep or Save File when downloading the .deb, jar, .tar.gz, .tar.xz, .AppImage and other files.

Table of Contents

[Copyright             2](#part0001.xhtml___RefHeading___Toc4389_3642366430)

[Disclaimer             3](#part0002.xhtml___RefHeading___Toc4391_3642366430)

[Trademark             4](#part0003.xhtml___RefHeading___Toc4393_3642366430)

[Acknowledgements             5](#part0004.xhtml___RefHeading___Toc4395_3642366430)

[Install Machine Details             6](#part0005.xhtml___RefHeading___Toc4397_3642366430)

[Introduction             8](#part0006.xhtml___RefHeading___Toc4399_3642366430)

[Antivirus             33](#part0008.xhtml___RefHeading___Toc4401_3642366430)

[ClamAV             34](#part0009.xhtml___RefHeading___Toc4403_3642366430)

[ClamAV Install Using apt Command Line             34](#part0009.xhtml___RefHeading___Toc4405_3642366430)

[ClamAV Realtime             35](#part0010.xhtml___RefHeading___Toc4407_3642366430)

[ClamAV Realtime Using apt & systemctl Command Line              35](#part0010.xhtml___RefHeading___Toc4409_3642366430)

[ClamTK             38](#part0013.xhtml___RefHeading___Toc4411_3642366430)

[ClamTK Install Using Software Manager             38](#part0013.xhtml___RefHeading___Toc4413_3642366430)

[ClamTK Install Using apt Command Line             39](#part0014.xhtml___RefHeading___Toc4415_3642366430)

[ClamTK Install Using flatpak Command Line             40](#part0015.xhtml___RefHeading___Toc4417_3642366430)

[Audio Editors             41](#part0016.xhtml___RefHeading___Toc4419_3642366430)

[Audacity             42](#part0017.xhtml___RefHeading___Toc4421_3642366430)

[Audacity Install Using Software Manager             42](#part0017.xhtml___RefHeading___Toc4423_3642366430)

[Audacity Install Using apt Command Line             43](#part0018.xhtml___RefHeading___Toc4425_3642366430)

[Audacity Install Using flatpak Command Line             44](#part0019.xhtml___RefHeading___Toc4427_3642366430)

[Audacity Install Using Snap Store             45](#part0020.xhtml___RefHeading___Toc4429_3642366430)

[Audacity Install Using snap Command Line             46](#part0021.xhtml___RefHeading___Toc4431_3642366430)

[Ardour             47](#part0022.xhtml___RefHeading___Toc4433_3642366430)

[Ardour Install Using Software Manager             47](#part0022.xhtml___RefHeading___Toc4435_3642366430)

[Ardour Install Using apt Command Line             48](#part0023.xhtml___RefHeading___Toc4437_3642366430)

[Ardour Install Using flatpak Command Line             49](#part0024.xhtml___RefHeading___Toc4439_3642366430)

[LMMS             50](#part0025.xhtml___RefHeading___Toc4441_3642366430)

[LMMS Install Using Software Manager             50](#part0025.xhtml___RefHeading___Toc4443_3642366430)

[LMMS Install Using apt Command Line             51](#part0026.xhtml___RefHeading___Toc4445_3642366430)

[LMMS Install Using flatpak Command Line             52](#part0027.xhtml___RefHeading___Toc4447_3642366430)

[CD/DVD Makers             53](#part0028.xhtml___RefHeading___Toc4449_3642366430)

[Brasero             53](#part0028.xhtml___RefHeading___Toc4461_3642366430)

[Brasero Install Using Software Manager             53](#part0028.xhtml___RefHeading___Toc4463_3642366430)

[Brasero Install Using apt Command Line             53](#part0028.xhtml___RefHeading___Toc4465_3642366430)

[K3b             53](#part0028.xhtml___RefHeading___Toc4467_3642366430)

[K3b Install Using Software Manager             53](#part0028.xhtml___RefHeading___Toc4469_3642366430)

[K3b Install Using apt Command Line             53](#part0028.xhtml___RefHeading___Toc4471_3642366430)

[XFBurn             53](#part0028.xhtml___RefHeading___Toc4473_3642366430)

[XFBurn Install Using Software Manager             53](#part0028.xhtml___RefHeading___Toc4475_3642366430)

[XFBurn Install Using apt Command Line             53](#part0028.xhtml___RefHeading___Toc4477_3642366430)

[Brasero             54](#part0029.xhtml___RefHeading___Toc4479_3642366430)

[Brasero Install Using Software Manager             54](#part0029.xhtml___RefHeading___Toc4481_3642366430)

[Brasero Install Using apt Command Line             55](#part0030.xhtml___RefHeading___Toc4483_3642366430)

[K3b             56](#part0031.xhtml___RefHeading___Toc4485_3642366430)

[K3b Install Using Software Manager             56](#part0031.xhtml___RefHeading___Toc4487_3642366430)

[K3b Install Using apt Command Line             57](#part0032.xhtml___RefHeading___Toc4489_3642366430)

[XFBurn             58](#part0033.xhtml___RefHeading___Toc4491_3642366430)

[XFBurn Install Using Software Manager             58](#part0033.xhtml___RefHeading___Toc4493_3642366430)

[XFBurn Install Using apt Command Line             59](#part0034.xhtml___RefHeading___Toc4495_3642366430)

[Cloud Backup             60](#part0035.xhtml___RefHeading___Toc4505_3642366430)

[Insync             61](#part0036.xhtml___RefHeading___Toc4507_3642366430)

[Insync Install Using .deb             61](#part0036.xhtml___RefHeading___Toc4509_3642366430)

[Insync Install Using apt Command Line             62](#part0037.xhtml___RefHeading___Toc4511_3642366430)

[overGrive             66](#part0041.xhtml___RefHeading___Toc4513_3642366430)

[overGrive Install Using .deb             66](#part0041.xhtml___RefHeading___Toc4515_3642366430)

[Cloud Office Suites             67](#part0042.xhtml___RefHeading___Toc4517_3642366430)

[Google Docs             68](#part0043.xhtml___RefHeading___Toc4519_3642366430)

[Google Docs Access             68](#part0043.xhtml___RefHeading___Toc4521_3642366430)

[Microsoft Office 365             69](#part0044.xhtml___RefHeading___Toc4523_3642366430)

[Microsoft Office 365 Access             69](#part0044.xhtml___RefHeading___Toc4525_3642366430)

[Zoho Docs             70](#part0045.xhtml___RefHeading___Toc4527_3642366430)

[Zoho Docs Access             70](#part0045.xhtml___RefHeading___Toc4529_3642366430)

[Communication             71](#part0046.xhtml___RefHeading___Toc4531_3642366430)

[Discord             73](#part0047.xhtml___RefHeading___Toc4533_3642366430)

[Discord Install Using Software Manager             73](#part0047.xhtml___RefHeading___Toc4535_3642366430)

[Discord Install Using flatpak Command Line             74](#part0048.xhtml___RefHeading___Toc4537_3642366430)

[Discord Install Using Snap Store             75](#part0049.xhtml___RefHeading___Toc4539_3642366430)

[Discord Install Using snap Command Line             76](#part0050.xhtml___RefHeading___Toc4541_3642366430)

[Discord Install Using .deb             77](#part0051.xhtml___RefHeading___Toc4543_3642366430)

[Ferdium             78](#part0052.xhtml___RefHeading___Toc4545_3642366430)

[Ferdium Install Using Software Manager             78](#part0052.xhtml___RefHeading___Toc4547_3642366430)

[Ferdium Install Using flatpak Command Line             79](#part0053.xhtml___RefHeading___Toc4549_3642366430)

[Ferdium Install Using Snap Store             80](#part0054.xhtml___RefHeading___Toc4551_3642366430)

[Ferdium Install Using snap Command Line             81](#part0055.xhtml___RefHeading___Toc4553_3642366430)

[Ferdium Install Using .deb             82](#part0056.xhtml___RefHeading___Toc4555_3642366430)

[Pidgin             83](#part0057.xhtml___RefHeading___Toc4557_3642366430)

[Pidgin Install Using Software Manager             83](#part0057.xhtml___RefHeading___Toc4559_3642366430)

[Pidgin Install Using apt Command Line             84](#part0058.xhtml___RefHeading___Toc4561_3642366430)

[Pidgin Install Using flatpak Command Line             85](#part0059.xhtml___RefHeading___Toc4563_3642366430)

[Signal             86](#part0060.xhtml___RefHeading___Toc4565_3642366430)

[Signal Install Using Software Manager             86](#part0060.xhtml___RefHeading___Toc4567_3642366430)

[Signal Install Using flatpak Command Line             87](#part0061.xhtml___RefHeading___Toc4569_3642366430)

[Signal Install Using Snap Store             88](#part0062.xhtml___RefHeading___Toc4571_3642366430)

[Signal Install Using snap Command Line             89](#part0063.xhtml___RefHeading___Toc4573_3642366430)

[Telegram             90](#part0064.xhtml___RefHeading___Toc4575_3642366430)

[Telegram Install Using Software Manager             90](#part0064.xhtml___RefHeading___Toc4577_3642366430)

[Telegram Install Using flatpak Command Line             91](#part0065.xhtml___RefHeading___Toc4579_3642366430)

[Telegram Install Using Snap Store             92](#part0066.xhtml___RefHeading___Toc4581_3642366430)

[Telegram Install Using snap Command Line             93](#part0067.xhtml___RefHeading___Toc4583_3642366430)

[Cryptocurrency Wallets             94](#part0068.xhtml___RefHeading___Toc4585_3642366430)

[Coin             95](#part0069.xhtml___RefHeading___Toc4587_3642366430)

[Coin Install Using Snap Store             95](#part0069.xhtml___RefHeading___Toc4589_3642366430)

[Coin Install Using snap Command Line             96](#part0070.xhtml___RefHeading___Toc4591_3642366430)

[Exodus             97](#part0071.xhtml___RefHeading___Toc4593_3642366430)

[Exodus Install Using Software Manager             97](#part0071.xhtml___RefHeading___Toc4595_3642366430)

[Exodus Install Using flatpak Command Line             98](#part0072.xhtml___RefHeading___Toc4597_3642366430)

[Exodus Install Using .deb             99](#part0073.xhtml___RefHeading___Toc4599_3642366430)

[Guarda Wallet             100](#part0074.xhtml___RefHeading___Toc4601_3642366430)

[Guarda Install Using .deb             100](#part0074.xhtml___RefHeading___Toc4603_3642366430)

[Wasabi Wallet             101](#part0075.xhtml___RefHeading___Toc4605_3642366430)

[Wasabi Wallet Install Using Software Manager             101](#part0075.xhtml___RefHeading___Toc4607_3642366430)

[Wasabi Wallet Install Using flatpak Command Line              102](#part0076.xhtml___RefHeading___Toc4609_3642366430)

[Wasabi Wallet Install Using .deb             103](#part0077.xhtml___RefHeading___Toc4611_3642366430)

[Custom Kernels             104](#part0078.xhtml___RefHeading___Toc4613_3642366430)

[Liquorix             104](#part0078.xhtml___RefHeading___Toc4625_3642366430)

[Liquorix Install Using apt Command Line             104](#part0078.xhtml___RefHeading___Toc4627_3642366430)

[Xanmod Stable             104](#part0078.xhtml___RefHeading___Toc4629_3642366430)

[Xanmod Stable Install Using apt Command Line              104](#part0078.xhtml___RefHeading___Toc4631_3642366430)

[Liquorix             105](#part0079.xhtml___RefHeading___Toc4633_3642366430)

[Liquorix Install Using apt Command Line             105](#part0079.xhtml___RefHeading___Toc4635_3642366430)

[Xanmod Stable             107](#part0081.xhtml___RefHeading___Toc4637_3642366430)

[Xanmod Stable Install Using apt Command Line              107](#part0081.xhtml___RefHeading___Toc4639_3642366430)

[Data Recovery             113](#part0087.xhtml___RefHeading___Toc4641_3642366430)

[R-Linux             114](#part0088.xhtml___RefHeading___Toc4643_3642366430)

[R-Linux Install Using .deb             114](#part0088.xhtml___RefHeading___Toc4645_3642366430)

[Desktop Environments             115](#part0089.xhtml___RefHeading___Toc4647_3642366430)

[Tasksel             116](#part0090.xhtml___RefHeading___Toc4649_3642366430)

[Tasksel Install Using apt Command Line             116](#part0090.xhtml___RefHeading___Toc4651_3642366430)

[KDE Plasma             117](#part0091.xhtml___RefHeading___Toc4653_3642366430)

[KDE Plasma Install Using apt Command Line             117](#part0091.xhtml___RefHeading___Toc4655_3642366430)

[LXDE             118](#part0092.xhtml___RefHeading___Toc4657_3642366430)

[LXDE Install Using apt Command Line             118](#part0092.xhtml___RefHeading___Toc4659_3642366430)

[LXQT             119](#part0093.xhtml___RefHeading___Toc4661_3642366430)

[LXQT Install Using apt Command Line             119](#part0093.xhtml___RefHeading___Toc4663_3642366430)

[Gnome             120](#part0094.xhtml___RefHeading___Toc4665_3642366430)

[Gnome Install Using tasksel Command Line             120](#part0094.xhtml___RefHeading___Toc4667_3642366430)

[Download Managers             122](#part0096.xhtml___RefHeading___Toc4669_3642366430)

[FlareGet             123](#part0097.xhtml___RefHeading___Toc4671_3642366430)

[FlareGet Install Using .deb             123](#part0097.xhtml___RefHeading___Toc4673_3642366430)

[KGet             124](#part0098.xhtml___RefHeading___Toc4675_3642366430)

[KGet Install Using Software Manager             124](#part0098.xhtml___RefHeading___Toc4677_3642366430)

[KGet Install Using apt Command Line             125](#part0099.xhtml___RefHeading___Toc4679_3642366430)

[KGet Install Using flatpak Command Line             126](#part0100.xhtml___RefHeading___Toc4681_3642366430)

[Motrix             127](#part0101.xhtml___RefHeading___Toc4683_3642366430)

[Motrix Install Using Snap Store             127](#part0101.xhtml___RefHeading___Toc4685_3642366430)

[Motrix Install Using snap Command Line             128](#part0102.xhtml___RefHeading___Toc4687_3642366430)

[Motrix Install Using .deb             129](#part0103.xhtml___RefHeading___Toc4689_3642366430)

[Persepolis             130](#part0104.xhtml___RefHeading___Toc4693_3642366430)

[Persepolis Install Using apt Command Line             130](#part0104.xhtml___RefHeading___Toc4695_3642366430)

[uGet             131](#part0105.xhtml___RefHeading___Toc4697_3642366430)

[uGet Install Using Software Manager             131](#part0105.xhtml___RefHeading___Toc4699_3642366430)

[uGet Install Using apt Command Line             132](#part0106.xhtml___RefHeading___Toc4701_3642366430)

[Ebook Readers             133](#part0107.xhtml___RefHeading___Toc4705_3642366430)

[Calibre             135](#part0108.xhtml___RefHeading___Toc4707_3642366430)

[Calibre Install Using Software Manager             135](#part0108.xhtml___RefHeading___Toc4709_3642366430)

[Calibre Install Using apt Command Line             136](#part0109.xhtml___RefHeading___Toc4711_3642366430)

[Calibre Install Using flatpak Command Line             137](#part0110.xhtml___RefHeading___Toc4713_3642366430)

[Calibre Install Using Binary install Command Line              138](#part0111.xhtml___RefHeading___Toc4715_3642366430)

[FBReader             139](#part0112.xhtml___RefHeading___Toc4717_3642366430)

[FBReader Install Using Software Manager             139](#part0112.xhtml___RefHeading___Toc4719_3642366430)

[FBReader Install Using apt Command Line             140](#part0113.xhtml___RefHeading___Toc4721_3642366430)

[FBReader Install Using Snap Store             141](#part0114.xhtml___RefHeading___Toc4723_3642366430)

[FBReader Install Using snap Command Line             142](#part0115.xhtml___RefHeading___Toc4725_3642366430)

[Lucidor             143](#part0116.xhtml___RefHeading___Toc4727_3642366430)

[Lucidor Install Using .deb             143](#part0116.xhtml___RefHeading___Toc4729_3642366430)

[Okular             144](#part0117.xhtml___RefHeading___Toc4731_3642366430)

[Okular Install Using Software Manager             144](#part0117.xhtml___RefHeading___Toc4733_3642366430)

[Okular Install Using apt Command Line             145](#part0118.xhtml___RefHeading___Toc4735_3642366430)

[Okular Install Using flatpak Command Line             146](#part0119.xhtml___RefHeading___Toc4737_3642366430)

[Okular Install Using Snap Store             147](#part0120.xhtml___RefHeading___Toc4739_3642366430)

[Okular Install Using snap Command Line             148](#part0121.xhtml___RefHeading___Toc4741_3642366430)

[Bookworm             149](#part0122.xhtml___RefHeading___Toc4743_3642366430)

[Bookworm Install Using Software Manager             149](#part0122.xhtml___RefHeading___Toc4745_3642366430)

[Bookworm Install Using apt Command Line             150](#part0123.xhtml___RefHeading___Toc4747_3642366430)

[Bookworm Install Using flatpak Command Line151](#part0124.xhtml___RefHeading___Toc4749_3642366430)

[Elder Gaming             152](#part0125.xhtml___RefHeading___Toc4751_3642366430)

[DOSBox             153](#part0126.xhtml___RefHeading___Toc4753_3642366430)

[DOSBox Install Using Software Manager             153](#part0126.xhtml___RefHeading___Toc4755_3642366430)

[DOSBox Install Using apt Command Line             154](#part0127.xhtml___RefHeading___Toc4757_3642366430)

[DOSBox Install Using flatpak Command Line             155](#part0128.xhtml___RefHeading___Toc4759_3642366430)

[libopusfile0 Install Using apt Command Line             156](#part0129.xhtml___RefHeading___Toc4761_3642366430)

[Gnome Games App             157](#part0130.xhtml___RefHeading___Toc4763_3642366430)

[Gnome Games App Install Using Software Manager              157](#part0130.xhtml___RefHeading___Toc4765_3642366430)

[Gnome Games App Install Using apt Command Line              158](#part0131.xhtml___RefHeading___Toc4767_3642366430)

[Gnome Games App Install Using flatpak Command Line              159](#part0132.xhtml___RefHeading___Toc4769_3642366430)

[ScummVM             160](#part0133.xhtml___RefHeading___Toc4775_3642366430)

[ScummVM Install Using Software Manager             160](#part0133.xhtml___RefHeading___Toc4777_3642366430)

[ScummVM Install Using apt Command Line             161](#part0134.xhtml___RefHeading___Toc4779_3642366430)

[ScummVM Install Using flatpak Command Line162](#part0135.xhtml___RefHeading___Toc4781_3642366430)

[ScummVM Install Using Snap Store             163](#part0136.xhtml___RefHeading___Toc4783_3642366430)

[ScummVM Install Using snap Command Line             164](#part0137.xhtml___RefHeading___Toc4785_3642366430)

[File Compression and Extraction             165](#part0138.xhtml___RefHeading___Toc4787_3642366430)

[P7Zip-Desktop             166](#part0139.xhtml___RefHeading___Toc4789_3642366430)

[P7Zip-Desktop Install Using Snap Store             166](#part0139.xhtml___RefHeading___Toc4791_3642366430)

[P7Zip-Desktop Install Using snap Command Line              167](#part0140.xhtml___RefHeading___Toc4793_3642366430)

[Peazip             168](#part0141.xhtml___RefHeading___Toc4795_3642366430)

[Peazip Install Using Software Manager             168](#part0141.xhtml___RefHeading___Toc4797_3642366430)

[Peazip Install Using flatpak Command Line             169](#part0142.xhtml___RefHeading___Toc4799_3642366430)

[Peazip Install Using .deb             170](#part0143.xhtml___RefHeading___Toc4801_3642366430)

[Firewall             171](#part0144.xhtml___RefHeading___Toc4803_3642366430)

[All The Firewall Rules I Use             172](#part0145.xhtml___RefHeading___Toc4805_3642366430)

[TCP Ports             172](#part0145.xhtml___RefHeading___Toc4807_3642366430)

[UDP Ports             173](#part0146.xhtml___RefHeading___Toc4809_3642366430)

[UFW             174](#part0147.xhtml___RefHeading___Toc4811_3642366430)

[UFW Install Using apt Command Line             174](#part0147.xhtml___RefHeading___Toc4813_3642366430)

[UFW Enable             175](#part0148.xhtml___RefHeading___Toc4815_3642366430)

[UFW Add Single Port Rule             176](#part0149.xhtml___RefHeading___Toc4817_3642366430)

[UFW Add Multi Port Rule             177](#part0150.xhtml___RefHeading___Toc4819_3642366430)

[UFW Add Range Port Rule             178](#part0151.xhtml___RefHeading___Toc4821_3642366430)

[UFW Remove Port Rule             179](#part0152.xhtml___RefHeading___Toc4825_3642366430)

[Firewall Configuration             181](#part0154.xhtml___RefHeading___Toc4827_3642366430)

[Firewall Configuration Install Using Software Manager              181](#part0154.xhtml___RefHeading___Toc4829_3642366430)

[Firewall Configuration Install Using apt Command Line              182](#part0155.xhtml___RefHeading___Toc4831_3642366430)

[Firewall Configuration Add Single Port Rule             183](#part0156.xhtml___RefHeading___Toc4833_3642366430)

[Firewall Configuration Add Multi Port Rule             184](#part0157.xhtml___RefHeading___Toc4835_3642366430)

[Firewall Configuration Add Range Port Rule             185](#part0158.xhtml___RefHeading___Toc4837_3642366430)

[Firewall Configuration Add Rule From Report             186](#part0159.xhtml___RefHeading___Toc4839_3642366430)

[Firewall Configuration Remove Port Rule             187](#part0160.xhtml___RefHeading___Toc4841_3642366430)

[Game Engines             188](#part0161.xhtml___RefHeading___Toc4843_3642366430)

[Spring Engine             189](#part0162.xhtml___RefHeading___Toc4849_3642366430)

[Spring Engine Install Using Snap Store             189](#part0162.xhtml___RefHeading___Toc4851_3642366430)

[Spring Engine Install Using snap Command Line              190](#part0163.xhtml___RefHeading___Toc4853_3642366430)

[Unity             191](#part0164.xhtml___RefHeading___Toc4855_3642366430)

[Unity Install Using apt Command Line             191](#part0164.xhtml___RefHeading___Toc4857_3642366430)

[Home Living             194](#part0167.xhtml___RefHeading___Toc4859_3642366430)

[AnyMeal             196](#part0168.xhtml___RefHeading___Toc4861_3642366430)

[AnyMeal Install Using Software Manager             196](#part0168.xhtml___RefHeading___Toc4863_3642366430)

[AnyMeal Install Using apt Command Line             197](#part0169.xhtml___RefHeading___Toc4865_3642366430)

[AnyMeal Install Using .AppImage             198](#part0170.xhtml___RefHeading___Toc4867_3642366430)

[GnuCash             199](#part0171.xhtml___RefHeading___Toc4869_3642366430)

[GnuCash Install Using Software Manager             199](#part0171.xhtml___RefHeading___Toc4871_3642366430)

[GnuCash Install Using apt Command Line             200](#part0172.xhtml___RefHeading___Toc4873_3642366430)

[GnuCash Install Using flatpak Command Line                          201](#part0173.xhtml___RefHeading___Toc4875_3642366430)

[Gnome Recipes             202](#part0174.xhtml___RefHeading___Toc4877_3642366430)

[Gnome Recipes Install Using Software Manager              202](#part0174.xhtml___RefHeading___Toc4879_3642366430)

[Gnome Recipes Install Using apt Command Line              203](#part0175.xhtml___RefHeading___Toc4881_3642366430)

[Gnome Recipes Install Using flatpak Command Line              204](#part0176.xhtml___RefHeading___Toc4883_3642366430)

[Home Assistant             205](#part0177.xhtml___RefHeading___Toc4885_3642366430)

[Home Assistant Install Using Snap Store             205](#part0177.xhtml___RefHeading___Toc4887_3642366430)

[Home Assistant Install Using snap Command Line              206](#part0178.xhtml___RefHeading___Toc4889_3642366430)

[HomeBank             207](#part0179.xhtml___RefHeading___Toc4891_3642366430)

[HomeBank Install Using Software Manager             207](#part0179.xhtml___RefHeading___Toc4893_3642366430)

[HomeBank Install Using apt Command Line             208](#part0180.xhtml___RefHeading___Toc4895_3642366430)

[HomeBank Install Using flatpak Command Line              209](#part0181.xhtml___RefHeading___Toc4897_3642366430)

[Skrooge             210](#part0182.xhtml___RefHeading___Toc4899_3642366430)

[Skrooge Install Using Software Manager             210](#part0182.xhtml___RefHeading___Toc4901_3642366430)

[Skrooge Install Using apt Command Line             211](#part0183.xhtml___RefHeading___Toc4903_3642366430)

[Skrooge Install Using flatpak Command Line             212](#part0184.xhtml___RefHeading___Toc4905_3642366430)

[Sweet Home 3D             213](#part0185.xhtml___RefHeading___Toc4907_3642366430)

[Sweet Home 3D Install Using Software Manager              213](#part0185.xhtml___RefHeading___Toc4909_3642366430)

[Sweet Home 3D Install Using apt Command Line              214](#part0186.xhtml___RefHeading___Toc4911_3642366430)

[Sweet Home 3D Install Using Snap Store             215](#part0187.xhtml___RefHeading___Toc4913_3642366430)

[Sweet Home 3D Install Using snap Command Line              216](#part0188.xhtml___RefHeading___Toc4915_3642366430)

[Image Editors             217](#part0189.xhtml___RefHeading___Toc4917_3642366430)

[Blender             219](#part0190.xhtml___RefHeading___Toc4919_3642366430)

[Blender Install Using Software Manager             219](#part0190.xhtml___RefHeading___Toc4921_3642366430)

[Blender Install Using apt Command Line             220](#part0191.xhtml___RefHeading___Toc4923_3642366430)

[Blender Install Using flatpak Command Line             221](#part0192.xhtml___RefHeading___Toc4925_3642366430)

[Blender Install Using Snap Store             222](#part0193.xhtml___RefHeading___Toc4927_3642366430)

[Blender Install Using snap Command Line             223](#part0194.xhtml___RefHeading___Toc4929_3642366430)

[Gnu Image Manipulation Program             224](#part0195.xhtml___RefHeading___Toc4931_3642366430)

[Gnu Image Manipulation Program Install Using Software Manager              224](#part0195.xhtml___RefHeading___Toc4933_3642366430)

[Gnu Image Manipulation Program Install Using apt Command Line              225](#part0196.xhtml___RefHeading___Toc4935_3642366430)

[Gnu Image Manipulation Program Install Using flatpak Command Line              226](#part0197.xhtml___RefHeading___Toc4937_3642366430)

[Gnu Image Manipulation Program Install Using Snap Store              227](#part0198.xhtml___RefHeading___Toc4939_3642366430)

[Gnu Image Manipulation Program Install Using snap Command Line              228](#part0199.xhtml___RefHeading___Toc4941_3642366430)

[Inkscape             229](#part0200.xhtml___RefHeading___Toc4943_3642366430)

[Inkscape Install Using Software Manager             229](#part0200.xhtml___RefHeading___Toc4945_3642366430)

[Inkscape Install Using apt Command Line             230](#part0201.xhtml___RefHeading___Toc4947_3642366430)

[Inkscape Install Using flatpak Command Line                          231](#part0202.xhtml___RefHeading___Toc4949_3642366430)

[Inkscape Install Using Snap Store             232](#part0203.xhtml___RefHeading___Toc4951_3642366430)

[Inkscape Install Using snap Command Line             233](#part0204.xhtml___RefHeading___Toc4953_3642366430)

[Krita             234](#part0205.xhtml___RefHeading___Toc4955_3642366430)

[Krita Install Using Software Manager             234](#part0205.xhtml___RefHeading___Toc4957_3642366430)

[Krita Install Using apt Command Line             235](#part0206.xhtml___RefHeading___Toc4959_3642366430)

[Krita Install Using flatpak Command Line             236](#part0207.xhtml___RefHeading___Toc4961_3642366430)

[Krita Install Using Snap Store             237](#part0208.xhtml___RefHeading___Toc4963_3642366430)

[Krita Install Using snap Command Line             238](#part0209.xhtml___RefHeading___Toc4965_3642366430)

[Pinta             239](#part0210.xhtml___RefHeading___Toc4967_3642366430)

[Pinta Install Using Software Manager             239](#part0210.xhtml___RefHeading___Toc4969_3642366430)

[Pinta Install Using apt Command Line             240](#part0211.xhtml___RefHeading___Toc4971_3642366430)

[Pinta Install Using flatpak Command Line             241](#part0212.xhtml___RefHeading___Toc4973_3642366430)

[Pinta Install Using Snap Store             242](#part0213.xhtml___RefHeading___Toc4975_3642366430)

[Pinta Install Using snap Command Line             243](#part0214.xhtml___RefHeading___Toc4977_3642366430)

[Integrated Development Environment             244](#part0215.xhtml___RefHeading___Toc4979_3642366430)

[Atom             246](#part0216.xhtml___RefHeading___Toc4981_3642366430)

[Atom Install Using Software Manager             246](#part0216.xhtml___RefHeading___Toc4983_3642366430)

[Atom Install Using flatpak Command Line             247](#part0217.xhtml___RefHeading___Toc4985_3642366430)

[Atom Install Using .deb             248](#part0218.xhtml___RefHeading___Toc4987_3642366430)

[Apache NetBeans             249](#part0219.xhtml___RefHeading___Toc4989_3642366430)

[Apache NetBeans Install Using Software Manager              249](#part0219.xhtml___RefHeading___Toc4991_3642366430)

[Apache NetBeans Install Using flatpak Command Line              250](#part0220.xhtml___RefHeading___Toc4993_3642366430)

[Apache NetBeans Install Using Snap Store             251](#part0221.xhtml___RefHeading___Toc4995_3642366430)

[Apache NetBeans Install Using snap Command Line              252](#part0222.xhtml___RefHeading___Toc4997_3642366430)

[Bluefish Editor             253](#part0223.xhtml___RefHeading___Toc4999_3642366430)

[Bluefish Editor Install Using Software Manager253](#part0223.xhtml___RefHeading___Toc5001_3642366430)

[Bluefish Editor Install Using apt Command Line              254](#part0224.xhtml___RefHeading___Toc5003_3642366430)

[Bluefish Editor Install Using flatpak Command Line              255](#part0225.xhtml___RefHeading___Toc5005_3642366430)

[Codium             256](#part0226.xhtml___RefHeading___Toc5007_3642366430)

[Codium Install Using Snap Store             256](#part0226.xhtml___RefHeading___Toc5009_3642366430)

[Codium Install Using snap Command Line             257](#part0227.xhtml___RefHeading___Toc5011_3642366430)

[Eclipse             258](#part0228.xhtml___RefHeading___Toc5013_3642366430)

[Eclipse Install Using Software Manager             258](#part0228.xhtml___RefHeading___Toc5015_3642366430)

[Eclipse Install Using flatpak Command Line             259](#part0229.xhtml___RefHeading___Toc5017_3642366430)

[Ecipse Install Using Snap Store             260](#part0230.xhtml___RefHeading___Toc5019_3642366430)

[Eclipse Install Using snap Command Line             261](#part0231.xhtml___RefHeading___Toc5021_3642366430)

[GNU Emacs             262](#part0232.xhtml___RefHeading___Toc5023_3642366430)

[GNU Emacs Install Using Software Manager             262](#part0232.xhtml___RefHeading___Toc5025_3642366430)

[GNU Emacs Install Using apt Command Line             263](#part0233.xhtml___RefHeading___Toc5027_3642366430)

[GNU Emacs Install Using flatpak Command Line              264](#part0234.xhtml___RefHeading___Toc5029_3642366430)

[Visual Studio Code             265](#part0235.xhtml___RefHeading___Toc5031_3642366430)

[Visual Studio Code Install Using Software Manager              265](#part0235.xhtml___RefHeading___Toc5033_3642366430)

[Visual Studio Code Install Using flatpak Command Line              266](#part0236.xhtml___RefHeading___Toc5035_3642366430)

[Visual Studio Code Install Using Snap Store             267](#part0237.xhtml___RefHeading___Toc5037_3642366430)

[Visual Studio Code Install Using snap Command Line              268](#part0238.xhtml___RefHeading___Toc5039_3642366430)

[Media Players             269](#part0239.xhtml___RefHeading___Toc5041_3642366430)

[Haruna             270](#part0240.xhtml___RefHeading___Toc5043_3642366430)

[Haruna Install Using Software Manager             270](#part0240.xhtml___RefHeading___Toc5045_3642366430)

[Haruna Install Using flatpak Command Line             271](#part0241.xhtml___RefHeading___Toc5047_3642366430)

[Parole             272](#part0242.xhtml___RefHeading___Toc5049_3642366430)

[Parole Install Using Software Manager             272](#part0242.xhtml___RefHeading___Toc5051_3642366430)

[Parole Install Using apt Command Line             273](#part0243.xhtml___RefHeading___Toc5053_3642366430)

[SMPlayer             274](#part0244.xhtml___RefHeading___Toc5055_3642366430)

[SMPlayer Install Using Software Manager             274](#part0244.xhtml___RefHeading___Toc5057_3642366430)

[SMPlayer Install Using apt Command Line             275](#part0245.xhtml___RefHeading___Toc5059_3642366430)

[SMPlayer Install Using flatpak Command Line                          276](#part0246.xhtml___RefHeading___Toc5061_3642366430)

[SMPlayer Install Using Snap Store             277](#part0247.xhtml___RefHeading___Toc5063_3642366430)

[SMPlayer Install Using snap Command Line             278](#part0248.xhtml___RefHeading___Toc5065_3642366430)

[VLC             279](#part0249.xhtml___RefHeading___Toc5067_3642366430)

[VLC Install Using Software Manager             279](#part0249.xhtml___RefHeading___Toc5069_3642366430)

[VLC Install Using apt Command Line             280](#part0250.xhtml___RefHeading___Toc5071_3642366430)

[VLC Install Using flatpak Command Line             281](#part0251.xhtml___RefHeading___Toc5073_3642366430)

[Modern Gaming             282](#part0252.xhtml___RefHeading___Toc5079_3642366430)

[WINE             284](#part0253.xhtml___RefHeading___Toc5081_3642366430)

[WINE Staging Install Using apt Command Line             284](#part0253.xhtml___RefHeading___Toc5083_3642366430)

[Lutris             291](#part0260.xhtml___RefHeading___Toc5085_3642366430)

[Lutris Install Using Software Manager             291](#part0260.xhtml___RefHeading___Toc5087_3642366430)

[Lutris Install Using apt Command Line             292](#part0261.xhtml___RefHeading___Toc5089_3642366430)

[Lutris Install Using Repository and apt Command Line              293](#part0262.xhtml___RefHeading___Toc5091_3642366430)

[Steam             294](#part0263.xhtml___RefHeading___Toc5093_3642366430)

[Steam Install Using Software Manager             294](#part0263.xhtml___RefHeading___Toc5095_3642366430)

[Steam Install Using apt Command Line             295](#part0264.xhtml___RefHeading___Toc5097_3642366430)

[Steam Install Using Snap Store             296](#part0265.xhtml___RefHeading___Toc5099_3642366430)

[Steam Install Using snap Command Line             297](#part0266.xhtml___RefHeading___Toc5101_3642366430)

[ProtonUp-Qt             298](#part0267.xhtml___RefHeading___Toc5105_3642366430)

[ProtonUp-Qt Install Using Software Manager             298](#part0267.xhtml___RefHeading___Toc5107_3642366430)

[ProtonUp-Qt Install Using flatpak Command Line              299](#part0268.xhtml___RefHeading___Toc5109_3642366430)

[ProtonUp-Qt Install Using .AppImage             300](#part0269.xhtml___RefHeading___Toc5111_3642366430)

[Proton-GE             301](#part0270.xhtml___RefHeading___Toc5113_3642366430)

[Proton-GE Lutris Install Using .tar.gz             301](#part0270.xhtml___RefHeading___Toc5115_3642366430)

[Proton-GE Steam Install Using .tar.gz             302](#part0271.xhtml___RefHeading___Toc5117_3642366430)

[WINE-GE             303](#part0272.xhtml___RefHeading___Toc5119_3642366430)

[WINE-GE Lutris Install Using .tar.xz             303](#part0272.xhtml___RefHeading___Toc5121_3642366430)

[DXVK             304](#part0273.xhtml___RefHeading___Toc5123_3642366430)

[DXVK Install Using .sh Command Line             304](#part0273.xhtml___RefHeading___Toc5125_3642366430)

[VKD3D             305](#part0274.xhtml___RefHeading___Toc5127_3642366430)

[VKD3D Install Using .sh Command Line             305](#part0274.xhtml___RefHeading___Toc5129_3642366430)

[Gnome Games             306](#part0275.xhtml___RefHeading___Toc5131_3642366430)

[Gnome Games Install Using apt Command Line              306](#part0275.xhtml___RefHeading___Toc5133_3642366430)

[KDE Games             307](#part0276.xhtml___RefHeading___Toc5135_3642366430)

[KDE Games Install Using apt Command Line             307](#part0276.xhtml___RefHeading___Toc5137_3642366430)

[Music On Demand Streaming             308](#part0277.xhtml___RefHeading___Toc5143_3642366430)

[Amazon Music Unlimited             309](#part0278.xhtml___RefHeading___Toc5145_3642366430)

[Amazon Music Unlimited Web Access             309](#part0278.xhtml___RefHeading___Toc5147_3642366430)

[Apple Music             310](#part0279.xhtml___RefHeading___Toc5149_3642366430)

[Apple Music Web Access             310](#part0279.xhtml___RefHeading___Toc5151_3642366430)

[Spotify             311](#part0280.xhtml___RefHeading___Toc5153_3642366430)

[Spotify Install Using Snap Store             311](#part0280.xhtml___RefHeading___Toc5155_3642366430)

[Spotify Install Using snap Command Line             312](#part0281.xhtml___RefHeading___Toc5157_3642366430)

[Spotify Web Access             313](#part0282.xhtml___RefHeading___Toc5159_3642366430)

[Tidal             314](#part0283.xhtml___RefHeading___Toc5161_3642366430)

[Tidal Web Access             314](#part0283.xhtml___RefHeading___Toc5163_3642366430)

[Youtube Music             315](#part0284.xhtml___RefHeading___Toc5165_3642366430)

[Youtube Music Web Access             315](#part0284.xhtml___RefHeading___Toc5167_3642366430)

[Music Players             316](#part0285.xhtml___RefHeading___Toc5169_3642366430)

[Audacious             318](#part0286.xhtml___RefHeading___Toc5171_3642366430)

[Audacious Install Using Software Manager             318](#part0286.xhtml___RefHeading___Toc5173_3642366430)

[Audacious Install Using apt Command Line             319](#part0287.xhtml___RefHeading___Toc5175_3642366430)

[Audacious Install Using flatpak Command Line320](#part0288.xhtml___RefHeading___Toc5177_3642366430)

[Clementine             321](#part0289.xhtml___RefHeading___Toc5179_3642366430)

[Clementine Install Using Software Manager             321](#part0289.xhtml___RefHeading___Toc5181_3642366430)

[Clementine Install Using apt Command Line             322](#part0290.xhtml___RefHeading___Toc5183_3642366430)

[Clementine Install Using flatpak Command Line              323](#part0291.xhtml___RefHeading___Toc5185_3642366430)

[Clementine Install Using Snap Store             324](#part0292.xhtml___RefHeading___Toc5187_3642366430)

[Clementine Install Using snap Command Line                          325](#part0293.xhtml___RefHeading___Toc5189_3642366430)

[Deadbeef-vs             326](#part0294.xhtml___RefHeading___Toc5191_3642366430)

[Deadbeef-vs Install Using Snap Store             326](#part0294.xhtml___RefHeading___Toc5193_3642366430)

[Deadbeef-vs Install Using snap Command Line327](#part0295.xhtml___RefHeading___Toc5195_3642366430)

[Lollypop             328](#part0296.xhtml___RefHeading___Toc5197_3642366430)

[Lollypop Install Using Software Manager             328](#part0296.xhtml___RefHeading___Toc5199_3642366430)

[Lollypop Install Using apt Command Line             329](#part0297.xhtml___RefHeading___Toc5201_3642366430)

[Lollypop Install Using flatpak Command Line             330](#part0298.xhtml___RefHeading___Toc5203_3642366430)

[Rhythmbox             331](#part0299.xhtml___RefHeading___Toc5205_3642366430)

[Rhythmbox Install Using Software Manager             331](#part0299.xhtml___RefHeading___Toc5207_3642366430)

[Rhythmbox Install Using apt Command Line             332](#part0300.xhtml___RefHeading___Toc5209_3642366430)

[Rhythmbox Install Using flatpak Command Line              333](#part0301.xhtml___RefHeading___Toc5211_3642366430)

[Office Suites             334](#part0302.xhtml___RefHeading___Toc5213_3642366430)

[LibreOffice             335](#part0303.xhtml___RefHeading___Toc5215_3642366430)

[LibreOffice Install Using Software Manager             335](#part0303.xhtml___RefHeading___Toc5217_3642366430)

[LibreOffice Install Using apt Command Line             336](#part0304.xhtml___RefHeading___Toc5219_3642366430)

[LibreOffice Install Using flatpak Command Line              337](#part0305.xhtml___RefHeading___Toc5221_3642366430)

[LibreOffice Install Using Snap Store             338](#part0306.xhtml___RefHeading___Toc5223_3642366430)

[LibreOffice Install Using snap Command Line                          339](#part0307.xhtml___RefHeading___Toc5225_3642366430)

[OnlyOffice             340](#part0308.xhtml___RefHeading___Toc5227_3642366430)

[OnlyOffice Install Using Software Manager             340](#part0308.xhtml___RefHeading___Toc5229_3642366430)

[OnlyOffice Install Using flatpak Command Line341](#part0309.xhtml___RefHeading___Toc5231_3642366430)

[OnlyOffice Install Using Snap Store             342](#part0310.xhtml___RefHeading___Toc5233_3642366430)

[OnlyOffice Install Using snap Command Line             343](#part0311.xhtml___RefHeading___Toc5235_3642366430)

[OnlyOffice Install Using .deb             344](#part0312.xhtml___RefHeading___Toc5237_3642366430)

[OpenOffice             345](#part0313.xhtml___RefHeading___Toc5239_3642366430)

[OpenOffice Install Using .AppImage             345](#part0313.xhtml___RefHeading___Toc5241_3642366430)

[Partition Managers             346](#part0314.xhtml___RefHeading___Toc5243_3642366430)

[GParted             347](#part0315.xhtml___RefHeading___Toc5245_3642366430)

[GParted Install Using Software Manager             347](#part0315.xhtml___RefHeading___Toc5247_3642366430)

[GParted Install Using apt Command Line             348](#part0316.xhtml___RefHeading___Toc5249_3642366430)

[KDE Partition Manager             349](#part0317.xhtml___RefHeading___Toc5251_3642366430)

[KDE Partition Manager Install Using Software Manager              349](#part0317.xhtml___RefHeading___Toc5253_3642366430)

[KDE Partition Manager Install Using apt Command Line              350](#part0318.xhtml___RefHeading___Toc5255_3642366430)

[Password Managers             351](#part0319.xhtml___RefHeading___Toc5257_3642366430)

[1Password             353](#part0320.xhtml___RefHeading___Toc5259_3642366430)

[1Password Install Using .deb             353](#part0320.xhtml___RefHeading___Toc5261_3642366430)

[Bitwarden             354](#part0321.xhtml___RefHeading___Toc5263_3642366430)

[Bitwarden Install Using Software Manager             354](#part0321.xhtml___RefHeading___Toc5265_3642366430)

[Bitwarden Install Using flatpak Command Line             355](#part0322.xhtml___RefHeading___Toc5267_3642366430)

[Bitwarden Install Using Snap Store             356](#part0323.xhtml___RefHeading___Toc5269_3642366430)

[Bitwarden Install Using snap Command Line             357](#part0324.xhtml___RefHeading___Toc5271_3642366430)

[Bitwarden Install Using .deb             358](#part0325.xhtml___RefHeading___Toc5273_3642366430)

[Buttercup             359](#part0326.xhtml___RefHeading___Toc5275_3642366430)

[Buttercup Install Using .AppImage             359](#part0326.xhtml___RefHeading___Toc5277_3642366430)

[KeePassXC             360](#part0327.xhtml___RefHeading___Toc5279_3642366430)

[KeePassXC Install Using Software Manager             360](#part0327.xhtml___RefHeading___Toc5281_3642366430)

[KeePassXC Install Using apt Command Line             361](#part0328.xhtml___RefHeading___Toc5283_3642366430)

[KeePassXC Install Using flatpak Command Line              362](#part0329.xhtml___RefHeading___Toc5285_3642366430)

[KeePassXC Install Using Snap Store             363](#part0330.xhtml___RefHeading___Toc5287_3642366430)

[KeePassXC Install Using snap Command Line                          364](#part0331.xhtml___RefHeading___Toc5289_3642366430)

[LastPass             365](#part0332.xhtml___RefHeading___Toc5291_3642366430)

[LastPass Universal Linux Installer Install Using .sh Command Line              365](#part0332.xhtml___RefHeading___Toc5293_3642366430)

[Remote Working             367](#part0333.xhtml___RefHeading___Toc5295_3642366430)

[Citrix             368](#part0334.xhtml___RefHeading___Toc5297_3642366430)

[Citrix Install Using .deb             368](#part0334.xhtml___RefHeading___Toc5299_3642366430)

[Microsoft Teams             370](#part0335.xhtml___RefHeading___Toc5301_3642366430)

[Microsoft Teams Install Using Snap Store             370](#part0335.xhtml___RefHeading___Toc5303_3642366430)

[Microsoft Teams Install Using snap Command Line              371](#part0336.xhtml___RefHeading___Toc5305_3642366430)

[Slack             372](#part0337.xhtml___RefHeading___Toc5307_3642366430)

[Slack Install Using .deb             372](#part0337.xhtml___RefHeading___Toc5309_3642366430)

[Zoom             373](#part0338.xhtml___RefHeading___Toc5311_3642366430)

[Zoom Install Using .deb             373](#part0338.xhtml___RefHeading___Toc5313_3642366430)

[Sandbox             375](#part0339.xhtml___RefHeading___Toc5315_3642366430)

[Firejail             376](#part0340.xhtml___RefHeading___Toc5317_3642366430)

[Firejail Install Using Software Manager             376](#part0340.xhtml___RefHeading___Toc5319_3642366430)

[Firejail Install Using apt Command Line             377](#part0341.xhtml___RefHeading___Toc5321_3642366430)

[Firetools             378](#part0342.xhtml___RefHeading___Toc5323_3642366430)

[Firetools Install Using Software Manager             378](#part0342.xhtml___RefHeading___Toc5325_3642366430)

[Firetools Install Using apt Command Line             379](#part0343.xhtml___RefHeading___Toc5327_3642366430)

[Software Distribution             380](#part0344.xhtml___RefHeading___Toc5329_3642366430)

[AppImageLauncher             382](#part0345.xhtml___RefHeading___Toc5331_3642366430)

[AppImageLauncher Install Using apt Command Line              382](#part0345.xhtml___RefHeading___Toc5333_3642366430)

[AppImage Launcher Install Using .deb             383](#part0346.xhtml___RefHeading___Toc5335_3642366430)

[Flatpak             384](#part0347.xhtml___RefHeading___Toc5337_3642366430)

[Flatpak Install Using apt Command Line             384](#part0347.xhtml___RefHeading___Toc5339_3642366430)

[Flathub             385](#part0348.xhtml___RefHeading___Toc5341_3642366430)

[Flathub Repo Add Using flatpak Command Line              385](#part0348.xhtml___RefHeading___Toc5343_3642366430)

[Snap             386](#part0349.xhtml___RefHeading___Toc5345_3642366430)

[Snap Install Using apt Command Line             386](#part0349.xhtml___RefHeading___Toc5347_3642366430)

[Snap Store             388](#part0351.xhtml___RefHeading___Toc5349_3642366430)

[Snap Store Install Using snap Command Line                          388](#part0351.xhtml___RefHeading___Toc5351_3642366430)

[Java             389](#part0352.xhtml___RefHeading___Toc5353_3642366430)

[Java Install Using .deb             389](#part0352.xhtml___RefHeading___Toc5355_3642366430)

[Ocs-url             390](#part0353.xhtml___RefHeading___Toc5357_3642366430)

[Ocs-url Install Using .deb             390](#part0353.xhtml___RefHeading___Toc5359_3642366430)

[Open Java             391](#part0354.xhtml___RefHeading___Toc5361_3642366430)

[Open Java JRE and JDK Install Using apt Command Line              391](#part0354.xhtml___RefHeading___Toc5363_3642366430)

[deb-get             392](#part0355.xhtml___RefHeading___Toc5365_3642366430)

[deb-get Install using curl Command Line             392](#part0355.xhtml___RefHeading___Toc5367_3642366430)

[App Outlet             394](#part0357.xhtml___RefHeading___Toc5369_3642366430)

[App Outlet Install Using .deb             394](#part0357.xhtml___RefHeading___Toc5371_3642366430)

[pacstall             395](#part0358.xhtml___RefHeading___Toc5373_3642366430)

[pacstall Install Using curl Command Line             395](#part0358.xhtml___RefHeading___Toc5375_3642366430)

[Streaming             396](#part0359.xhtml___RefHeading___Toc5377_3642366430)

[OBS Studio             397](#part0360.xhtml___RefHeading___Toc5379_3642366430)

[OBS Studio Install Using Software Manager             397](#part0360.xhtml___RefHeading___Toc5381_3642366430)

[OBS Studio Install Using apt Command Line             398](#part0361.xhtml___RefHeading___Toc5383_3642366430)

[OBS Studio Install Using flatpak Command Line              399](#part0362.xhtml___RefHeading___Toc5385_3642366430)

[OBS Studio Install Using Snap Store             400](#part0363.xhtml___RefHeading___Toc5387_3642366430)

[OBS Studio Install Using snap Command Line                          401](#part0364.xhtml___RefHeading___Toc5389_3642366430)

[OBS Studio Install deb-get Command Line             402](#part0365.xhtml___RefHeading___Toc5391_3642366430)

[Owncast             403](#part0366.xhtml___RefHeading___Toc5393_3642366430)

[Owncast Install Using curl Command Line             403](#part0366.xhtml___RefHeading___Toc5395_3642366430)

[System Cleaners             404](#part0367.xhtml___RefHeading___Toc5397_3642366430)

[Bleachbit             406](#part0368.xhtml___RefHeading___Toc5399_3642366430)

[Bleachbit Install Using Software Manager             406](#part0368.xhtml___RefHeading___Toc5401_3642366430)

[Bleachhbit Install Using apt Command Line             407](#part0369.xhtml___RefHeading___Toc5403_3642366430)

[Czkawka             408](#part0370.xhtml___RefHeading___Toc5405_3642366430)

[Czkawka Install Using Software Manager             408](#part0370.xhtml___RefHeading___Toc5407_3642366430)

[Czkawka Install Using flatpak Command Line                          409](#part0371.xhtml___RefHeading___Toc5409_3642366430)

[Czkawka Install Using Snap Store             410](#part0372.xhtml___RefHeading___Toc5411_3642366430)

[Czkawka Install Using snap Command Line             411](#part0373.xhtml___RefHeading___Toc5413_3642366430)

[FSlint Unofficial             412](#part0374.xhtml___RefHeading___Toc5415_3642366430)

[FSlint Unofficial Install Using Snap Store             412](#part0374.xhtml___RefHeading___Toc5417_3642366430)

[FSlint Unofficial Install Using snap Command Line              413](#part0375.xhtml___RefHeading___Toc5419_3642366430)

[Stacer             414](#part0376.xhtml___RefHeading___Toc5421_3642366430)

[Stacer Install Using Software Manager             414](#part0376.xhtml___RefHeading___Toc5423_3642366430)

[Stacer Install Using apt Command Line             415](#part0377.xhtml___RefHeading___Toc5425_3642366430)

[Synaptic Package Manager             416](#part0378.xhtml___RefHeading___Toc5427_3642366430)

[Synpatic Package Manager Install Using Software Manager              416](#part0378.xhtml___RefHeading___Toc5429_3642366430)

[Synaptic Package Manager Install Using apt Command Line              417](#part0379.xhtml___RefHeading___Toc5431_3642366430)

[Sweeper             418](#part0380.xhtml___RefHeading___Toc5433_3642366430)

[Sweeper Install Using Software Manager             418](#part0380.xhtml___RefHeading___Toc5435_3642366430)

[Sweeper Install Using apt Command Line             419](#part0381.xhtml___RefHeading___Toc5437_3642366430)

[System Settings             420](#part0382.xhtml___RefHeading___Toc5439_3642366430)

[32 Bit Architecture             423](#part0383.xhtml___RefHeading___Toc5441_3642366430)

[32 Bit Architecture Install Using apt Command Line              423](#part0383.xhtml___RefHeading___Toc5443_3642366430)

[Alternative DNS Servers             424](#part0384.xhtml___RefHeading___Toc5445_3642366430)

[Alternative DNS Services Setup Using Network424](#part0384.xhtml___RefHeading___Toc5447_3642366430)

[List of Other Alternate DNS Services             427](#part0387.xhtml___RefHeading___Toc5449_3642366430)

[CleanBrowsing             427](#part0387.xhtml___RefHeading___Toc5451_3642366430)

[FOURTHESTATE             427](#part0387.xhtml___RefHeading___Toc5453_3642366430)

[DNS.WATCH             427](#part0387.xhtml___RefHeading___Toc5455_3642366430)

[quad9             428](#part0387.xhtml___RefHeading___Toc5457_3642366430)

[Auto Mount Disks             429](#part0388.xhtml___RefHeading___Toc5459_3642366430)

[Auto Mount Disks Using Disks             429](#part0388.xhtml___RefHeading___Toc5461_3642366430)

[Graphics Drivers             430](#part0389.xhtml___RefHeading___Toc5463_3642366430)

[AMD Graphics Drivers Install Using apt Command Line              430](#part0389.xhtml___RefHeading___Toc5465_3642366430)

[AMD Graphics Driver Default Using ppa-purge Command Line              432](#part0391.xhtml___RefHeading___Toc5467_3642366430)

[Nvidia Graphics Driver Install Using Software Manager              434](#part0393.xhtml___RefHeading___Toc5469_3642366430)

[Nvidia Graphics Driver Install Using apt Command Line              435](#part0394.xhtml___RefHeading___Toc5471_3642366430)

[Mousepad             436](#part0395.xhtml___RefHeading___Toc5473_3642366430)

[Mousepad Install Using Software Manager             436](#part0395.xhtml___RefHeading___Toc5475_3642366430)

[Mousepad Install Using apt Command Line             437](#part0396.xhtml___RefHeading___Toc5477_3642366430)

[Mouse Speed             438](#part0397.xhtml___RefHeading___Toc5479_3642366430)

[Setting Mouse Speed to Max             438](#part0397.xhtml___RefHeading___Toc5481_3642366430)

[Night Light             439](#part0398.xhtml___RefHeading___Toc5483_3642366430)

[Setting Up Night Light (Blue Light Protection)                          439](#part0398.xhtml___RefHeading___Toc5485_3642366430)

[Possible Intel Sound Crackle Fix             440](#part0399.xhtml___RefHeading___Toc5487_3642366430)

[Possible Intel Sound Crackle Fix Using echo Command Line              440](#part0399.xhtml___RefHeading___Toc5489_3642366430)

[Purge PPA’s             441](#part0400.xhtml___RefHeading___Toc5491_3642366430)

[Purge PPA’s Using Software Sources             441](#part0400.xhtml___RefHeading___Toc5493_3642366430)

[PPA Purge Install             442](#part0401.xhtml___RefHeading___Toc5495_3642366430)

[Purge PPA’s Using ppa-purge Command Line                          443](#part0402.xhtml___RefHeading___Toc5497_3642366430)

[Set Default Application             444](#part0403.xhtml___RefHeading___Toc5499_3642366430)

[Set Default Application for Category             444](#part0403.xhtml___RefHeading___Toc5501_3642366430)

[Set Default Application Per File Extension             445](#part0404.xhtml___RefHeading___Toc5503_3642366430)

[Startup Applications             446](#part0405.xhtml___RefHeading___Toc5505_3642366430)

[Startup Applications Using Installed Applications              446](#part0405.xhtml___RefHeading___Toc5507_3642366430)

[Startup Applications Using Custom Commands447](#part0406.xhtml___RefHeading___Toc5509_3642366430)

[Uninstalling Applications             448](#part0407.xhtml___RefHeading___Toc5511_3642366430)

[Uninstall Software Manager Applications             448](#part0407.xhtml___RefHeading___Toc5513_3642366430)

[Uninstall apt Command Line Applications             449](#part0408.xhtml___RefHeading___Toc5515_3642366430)

[Uninstall Snap Store Installed Applications             450](#part0409.xhtml___RefHeading___Toc5517_3642366430)

[Uninstall snap Command Line Applications             451](#part0410.xhtml___RefHeading___Toc5519_3642366430)

[Uninstalling deb-get Command Line Applications              452](#part0411.xhtml___RefHeading___Toc5521_3642366430)

[Updating Linux Mint 21             453](#part0412.xhtml___RefHeading___Toc5523_3642366430)

[Updating Linux Mint 21 Using Update Manager453](#part0412.xhtml___RefHeading___Toc5525_3642366430)

[Updating Linux Mint 21 Using apt Command Line              454](#part0413.xhtml___RefHeading___Toc5527_3642366430)

[Updating Linux Mint 21 Kernel Using Update Manager              455](#part0414.xhtml___RefHeading___Toc5529_3642366430)

[System Utilities             456](#part0415.xhtml___RefHeading___Toc5533_3642366430)

[Cpufetch             457](#part0416.xhtml___RefHeading___Toc5535_3642366430)

[Cpufetch Install Using apt Command Line             457](#part0416.xhtml___RefHeading___Toc5537_3642366430)

[CPU-X             458](#part0417.xhtml___RefHeading___Toc5539_3642366430)

[CPU-X Install Using .AppImage             458](#part0417.xhtml___RefHeading___Toc5541_3642366430)

[Gpustat             459](#part0418.xhtml___RefHeading___Toc5543_3642366430)

[Gpustat Install Using apt Command Line             459](#part0418.xhtml___RefHeading___Toc5545_3642366430)

[Hard Disk Sentinel             460](#part0419.xhtml___RefHeading___Toc5547_3642366430)

[Hard Disk Sentinel Install Using .tar.xz             460](#part0419.xhtml___RefHeading___Toc5549_3642366430)

[Neofetch             461](#part0420.xhtml___RefHeading___Toc5551_3642366430)

[Neofetch Install Using apt Command Line             461](#part0420.xhtml___RefHeading___Toc5553_3642366430)

[System Profiler and Benchmark             462](#part0421.xhtml___RefHeading___Toc5555_3642366430)

[System Profiler and Benchmark Install Using Software Manager              462](#part0421.xhtml___RefHeading___Toc5557_3642366430)

[System Profiler and Benchmark Install Using apt Command Line              463](#part0422.xhtml___RefHeading___Toc5559_3642366430)

[Psensor             464](#part0423.xhtml___RefHeading___Toc5561_3642366430)

[Psensor Install Using apt Command Line             464](#part0423.xhtml___RefHeading___Toc5563_3642366430)

[Video Editors             468](#part0427.xhtml___RefHeading___Toc5565_3642366430)

[Flowblade             470](#part0428.xhtml___RefHeading___Toc5567_3642366430)

[Flowblade Install Using Software Manager             470](#part0428.xhtml___RefHeading___Toc5569_3642366430)

[Flowblade Install Using apt Command Line             471](#part0429.xhtml___RefHeading___Toc5571_3642366430)

[Flowblade Install Using flatpak Command Line             472](#part0430.xhtml___RefHeading___Toc5573_3642366430)

[Kdenlive             473](#part0431.xhtml___RefHeading___Toc5575_3642366430)

[Kdenlive Install Using Software Manager             473](#part0431.xhtml___RefHeading___Toc5577_3642366430)

[Kdenlive Install Using apt Command Line             474](#part0432.xhtml___RefHeading___Toc5579_3642366430)

[Kdenlive Install Using flatpak Command Line             475](#part0433.xhtml___RefHeading___Toc5581_3642366430)

[Kdenlive Install Snap Store             476](#part0434.xhtml___RefHeading___Toc5583_3642366430)

[Kdenlive Install Using snap Command Line             477](#part0435.xhtml___RefHeading___Toc5585_3642366430)

[Openshot             478](#part0436.xhtml___RefHeading___Toc5587_3642366430)

[Openshot Install Using Software Manager             478](#part0436.xhtml___RefHeading___Toc5589_3642366430)

[Openshot Install Using apt Command Line             479](#part0437.xhtml___RefHeading___Toc5591_3642366430)

[Openshot Install Using flatpak Command Line                          480](#part0438.xhtml___RefHeading___Toc5593_3642366430)

[Openshot Install Using .AppImage             481](#part0439.xhtml___RefHeading___Toc5595_3642366430)

[Shotcut             482](#part0440.xhtml___RefHeading___Toc5597_3642366430)

[Shotcut Install Using Software Manager             482](#part0440.xhtml___RefHeading___Toc5599_3642366430)

[Shotcut Install Using apt Command Line             483](#part0441.xhtml___RefHeading___Toc5601_3642366430)

[Shotcut Install Using flatpak Command Line             484](#part0442.xhtml___RefHeading___Toc5603_3642366430)

[Shotcut Install Using Snap Store             485](#part0443.xhtml___RefHeading___Toc5605_3642366430)

[Shotcut Install Using snap Command Line             486](#part0444.xhtml___RefHeading___Toc5607_3642366430)

[Video On Demand Streaming             487](#part0445.xhtml___RefHeading___Toc5609_3642366430)

[Amazon Prime Video             488](#part0446.xhtml___RefHeading___Toc5611_3642366430)

[Amazon Prime Video Access             488](#part0446.xhtml___RefHeading___Toc5613_3642366430)

[Disney+             489](#part0447.xhtml___RefHeading___Toc5615_3642366430)

[Disney+ Access             489](#part0447.xhtml___RefHeading___Toc5617_3642366430)

[Netflix             490](#part0448.xhtml___RefHeading___Toc5619_3642366430)

[Netflix Access             490](#part0448.xhtml___RefHeading___Toc5621_3642366430)

[Paramount+             491](#part0449.xhtml___RefHeading___Toc5623_3642366430)

[Paramount+ Access             491](#part0449.xhtml___RefHeading___Toc5625_3642366430)

[Virtualization             492](#part0450.xhtml___RefHeading___Toc5627_3642366430)

[Virt-manager             493](#part0451.xhtml___RefHeading___Toc5629_3642366430)

[Virt-manager Install Using apt Command Line                          493](#part0451.xhtml___RefHeading___Toc5631_3642366430)

[Virtualbox             495](#part0453.xhtml___RefHeading___Toc5633_3642366430)

[Virtualbox Install Using Software Manager             495](#part0453.xhtml___RefHeading___Toc5635_3642366430)

[Virtualbox Install Using apt Command Line             496](#part0454.xhtml___RefHeading___Toc5637_3642366430)

[Web Browsers             497](#part0455.xhtml___RefHeading___Toc5639_3642366430)

[Firefox             499](#part0456.xhtml___RefHeading___Toc5641_3642366430)

[Firefox Install Using Software Manager             499](#part0456.xhtml___RefHeading___Toc5643_3642366430)

[Firefox Install Using apt Command Line             500](#part0457.xhtml___RefHeading___Toc5645_3642366430)

[Firefox Install Using flatpak Command Line             501](#part0458.xhtml___RefHeading___Toc5647_3642366430)

[Firefox Install Using Snap Store             502](#part0459.xhtml___RefHeading___Toc5649_3642366430)

[Firefox Install Using snap Command Line             503](#part0460.xhtml___RefHeading___Toc5651_3642366430)

[Firefox ESR             504](#part0461.xhtml___RefHeading___Toc5653_3642366430)

[Firefox ESR Install Using .tar.gz             504](#part0461.xhtml___RefHeading___Toc5655_3642366430)

[Chromium             505](#part0462.xhtml___RefHeading___Toc5657_3642366430)

[Chromium Install Using Snap Store             505](#part0462.xhtml___RefHeading___Toc5659_3642366430)

[Chromium Install Using snap Command Line             506](#part0463.xhtml___RefHeading___Toc5661_3642366430)

[Google Chrome             507](#part0464.xhtml___RefHeading___Toc5663_3642366430)

[Google Chrome Install Using apt Command Line              507](#part0464.xhtml___RefHeading___Toc5665_3642366430)

[Google Chrome Install Using .deb             510](#part0467.xhtml___RefHeading___Toc5667_3642366430)

[Microsoft Edge             511](#part0468.xhtml___RefHeading___Toc5669_3642366430)

[Microsoft Edge Install Using apt Command Line              511](#part0468.xhtml___RefHeading___Toc5671_3642366430)

[Microsoft Edge Install Using .deb             513](#part0470.xhtml___RefHeading___Toc5673_3642366430)

[Opera             514](#part0471.xhtml___RefHeading___Toc5675_3642366430)

[Opera Install Using Snap Store             514](#part0471.xhtml___RefHeading___Toc5677_3642366430)

[Opera Install Using snap Command Line             515](#part0472.xhtml___RefHeading___Toc5679_3642366430)

[Librewolf             516](#part0473.xhtml___RefHeading___Toc5681_3642366430)

[Librewolf Install Using Software Manager             516](#part0473.xhtml___RefHeading___Toc5683_3642366430)

[Librewolf Install Using apt Command Line             517](#part0474.xhtml___RefHeading___Toc5685_3642366430)

[Librewolf Install Using flatpak Command Line                          521](#part0478.xhtml___RefHeading___Toc5687_3642366430)

[Pale Moon             522](#part0479.xhtml___RefHeading___Toc5689_3642366430)

[Pale Moon Install Using apt Command Line             522](#part0479.xhtml___RefHeading___Toc5691_3642366430)

[World of Warcraft             525](#part0482.xhtml___RefHeading___Toc5693_3642366430)

[Possible Fix for Dark Screen In-Game Store Bug              526](#part0483.xhtml___RefHeading___Toc5695_3642366430)

[Direct X 12 Error             533](#part0490.xhtml___RefHeading___Toc5697_3642366430)

[How To Manually Install World of Warcraft Addons              535](#part0492.xhtml___RefHeading___Toc5699_3642366430)

[World of Warcraft Addon Managers             538](#part0495.xhtml___RefHeading___Toc5701_3642366430)

[Curseforge             539](#part0496.xhtml___RefHeading___Toc5703_3642366430)

[Curseforge Install Using .AppImage             539](#part0496.xhtml___RefHeading___Toc5705_3642366430)

[Curseforge Manually Add Game             540](#part0497.xhtml___RefHeading___Toc5707_3642366430)

[Curseforge Install Addon             541](#part0498.xhtml___RefHeading___Toc5721_3642366430)

[Curseforge Update Addon             542](#part0499.xhtml___RefHeading___Toc5723_3642366430)

[Curseforge Remove Addon             543](#part0500.xhtml___RefHeading___Toc5725_3642366430)

Antivirus

Antivirus software helps protect computers from malicious software, in addition to,

*   Multi threaded on demand file and directory scanning
*   Supports various formats with file archive extraction
*   Right click a directory to scan all within

This chapter covers,

ClamAV

*   ClamAV Install Using apt Command Line

ClamAV Realtime

*   ClamAV Realtime Using apt & systemctl Command Line

ClamTK

*   ClamTK Install Using Software Manager
*   ClamTK Install Using apt Command Line
*   ClamTK Install Using flatpak Command Line

ClamAV

ClamAV Install Using apt Command Line

![](Images/image00460.jpeg)

Open, Terminal

Type In,

sudo apt install clamav

Press, Enter

ClamAV Realtime

ClamAV Realtime Using apt & systemctl Command Line

![](Images/image00461.jpeg)

Open, Terminal

Type In,

sudo apt install clamav-daemon

Press, Enter

![](Images/image00462.jpeg)

Type In,

sudo systemctl enable clamav-daemon

Press, Enter

![](Images/image00463.jpeg)

Type In,

sudo systemctl start clamav-daemon

Press, Enter

ClamTK

ClamTK Install Using Software Manager

![](Images/image00464.jpeg)

Open, Software Manager

Type In,

clamtk

Click, ClamTk

Click, Install

ClamTK Install Using apt Command Line

![](Images/image00465.jpeg)

Open, Terminal

Type In,

sudo apt install clamtk

Press, Enter

ClamTK Install Using flatpak Command Line

![](Images/image00466.jpeg)

Open, Terminal

Type In,

flatpak install flathub com.gitlab.davem.ClamTk

Press, Enter

Audio Editors

Audio Editors are software permitting the editing and generation of audio and includes,

*   Ability to import and export different audio file formats
*   Converting between different file formats and sound quality
*   Recording audio from inputs, and storing them on the computer

This chapter covers,

Audacity

*   Audacity Install Using Software Manager
*   Audacity Install Using apt Command Line
*   Audacity Install Using flatpak Command Line
*   Audacity Install Using Snap Store
*   Audacity Install Using snap Command Line

Ardour

*   Ardour Install Using Software Manager
*   Ardour Install Using apt Command Line
*   Ardour Install Using flatpak Command Line

LMMS

*   LMMS Install Using Software Manger
*   LMMS Install Using apt Command Line
*   LMMS Install Using flatpak Command Line

Audacity

Audacity Install Using Software Manager

![](Images/image00467.jpeg)

Open, Software Manager

Type In,

audacity

Click, Audacity

Click, Install

Audacity Install Using apt Command Line

![](Images/image00468.jpeg)

Open, Terminal

Type In,

sudo apt install audacity

Press, Enter

Audacity Install Using flatpak Command Line

![](Images/image00469.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.audacityteam.Audacity

Press, Enter

Audacity Install Using Snap Store

![](Images/image00470.jpeg)

Open, Snap Store

Type In,

audacity

Click, Audacity

Click, Install

Audacity Install Using snap Command Line

![](Images/image00471.jpeg)

Open, Terminal

Type In,

sudo snap install audacity

Press, Enter

Ardour

Ardour Install Using Software Manager

![](Images/image00472.jpeg)

Open, Software Manager

Type In,

Ardour

Click, Ardour

Click, Install

Ardour Install Using apt Command Line

![](Images/image00473.jpeg)

Open, Terminal

Type In,

sudo apt install ardour

Press, Enter

Ardour Install Using flatpak Command Line

![](Images/image00474.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.ardour.Ardour

Press, Enter

LMMS

LMMS Install Using Software Manager

![](Images/image00475.jpeg)

Open, Software Manager

Type In,

LMMS

Click, LMMS

Click, Install

LMMS Install Using apt Command Line

![](Images/image00476.jpeg)

Open, Terminal

Type In,

sudo apt install lmms

Press, Enter

LMMS Install Using flatpak Command Line

![](Images/image00477.jpeg)

Open, Terminal

Type In,

flatpak install flathub io.lmms.LMMS

Press, Enter

CD/DVD Makers

CD/DVD Makers let the user backup their personal data and information to a CD or DVD, and arrive with features like,

*   Transfering Home Movies to CD’s and DVD’s
*   Taking Copyright Free Music to Listen to on the move
*   Backing up documents from old pc’s to new

This chapter covers,

Brasero

*   Brasero Install Using Software Manager
*   Brasero Install Using apt Command Line

K3b

*   K3b Install Using Software Manager
*   K3b Install Using apt Command Line

XFBurn

*   XFBurn Install Using Software Manager
*   XFBurn Install Using apt Command Line

Brasero

Brasero Install Using Software Manager

![](Images/image00478.jpeg)

Open, Software Manager

Type In,

brasero

Click, Brasero

Click, Install

Brasero Install Using apt Command Line

![](Images/image00479.jpeg)

Open, Terminal

Type In,

sudo apt install brasero

Press, Enter

K3b

K3b Install Using Software Manager

![](Images/image00480.jpeg)

Open, Software Manager

Type In,

k3b

Click, K3b

Click, Install

K3b Install Using apt Command Line

![](Images/image00481.jpeg)

Open, Terminal

Type In,

sudo apt install k3b

Press, Enter

XFBurn

XFBurn Install Using Software Manager

![](Images/image00482.jpeg)

Open, Software Manager

Type In,

xfburn

Click, XFBurn

Click, Install

XFBurn Install Using apt Command Line

![](Images/image00483.jpeg)

Open, Terminal

Type In,

sudo apt install xfburn

Press, Enter

Cloud Backup

Cloud Backup software enables the remote storage of files on a server and includes,

*   Automatically backup files and folders as they are created or edited
*   Mapping the cloud storage as a local drive using the WebDAV protocol
*   Setting the folders to synchronize to the remote server

This chapter covers,

Insync

*   Insync Install Using .deb
*   Insync Install Using apt Command Line

overGrive

*   overGrive Install Using .deb

Insync

Insync Install Using .deb

![](Images/image00484.jpeg)

Go to,

https://www.insynchq.com/downloads

Click, The Linux Tux symbol

Click, Download for Linux

Click, Installers

Click, 1st Box

Click, Linux Mint

Click, 2nd Box

Click, 20.x

Click, Download to Download insync_3.7.9.50368-focal_amd64.deb

Go to, Where insync_3.7.9.50368-focal_amd64.deb is downloaded

Double Click, insync_3.7.9.50368-focal_amd64.deb

Click, Install

Insync Install Using apt Command Line

![](Images/image00485.jpeg)

Open, Terminal

Type In,

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ACCAF35C

Press, Enter

![](Images/image00486.jpeg)

Type In,

sudo xed /etc/apt/sources.list.d/insync.list

![](Images/image00487.jpeg)

Type In,

deb http://apt.insync.io/mint vanessa non-free contrib

Click, Save

Press, CTRL + S

![](Images/image00488.jpeg)

Type In,

sudo apt update && sudo apt install insync

Press, Enter

overGrive

overGrive Install Using .deb

![](Images/image00489.jpeg)

Go to,

[https://www.thefanclub.co.za/overgrive](https://www.thefanclub.co.za/overgrive)

Click, overGrive 3.4.5 - Debian | Ubuntu | Mint to Download overgrive_3.4.5_all.deb

Go to, Where overgrive_3.4.5_all.deb is Downloaded

Double Click, overgrive_3.4.5_all.deb

Click, Install

Cloud Office Suites

Cloud Office Suites are web based versions of desktop office programs offering,

*   Auto-saving as creation or editing to the document is done
*   Extensions which can add new or augment existing functionality
*   Fully featured or stripped down alternatives, usually if a paid for tier is available

This chapter covers,

Google Docs

*   Google Docs Access

Microsoft Office 365

*   Microsoft Office 365 Access

Zoho Docs

*   Zoho Docs Access

Google Docs

Google Docs Access

![](Images/image00490.jpeg)

Go to,

https://www.google.com/intl/en-GB/docs/about/

Sign In, To access Google Docs

Microsoft Office 365

Microsoft Office 365 Access

![](Images/image00491.jpeg)

Go to,

https://www.office.com/

Sign In, To access Microsoft Office 365

Zoho Docs

Zoho Docs Access

![](Images/image00492.jpeg)

Go to,

[https://www.zoho.com/workdrive/](https://www.zoho.com/workdrive/)

Sign In, To access, Zoho Docs

Communication

Communication software lets beings talk to each other straight away with features like,

*   Letting beings experience themselves and share it with others
*   Sending documents, pictures and media files
*   Talking to each other by text, video, audio or combination of all three

This chapter covers,

Discord

*   Discord Install Using Software Manager
*   Discord Install Using flatpak Command Line
*   Discord Install Using Snap Store
*   Discord Install Using snap Command Line
*   Discord Install Using .deb

Ferdium

*   Ferdium Install Using Software Manager
*   Ferdium Install Using flatpak Command Line
*   Ferdium Install Using Snap Store
*   Ferdium Install Using snap Command Line
*   Ferdium Install Using .deb

Pidgin

*   Pidgin Install Using Software Manager
*   Pidgin Install Using apt Command Line
*   Pidgin Install Using flatpak Command Line

Signal

*   Signal Install Using Software Manager
*   Signal Install Using flatpak Command Line
*   Signal Install Using Snap Store
*   Signal Install Using snap Command Line

Telegram

*   Telegram Install Using Software Manager
*   Telegram Install Using flatpak Command Line
*   Telegram Install Using Snap Store
*   Telegram Install Using snap Command Line

Discord

Discord Install Using Software Manager

![](Images/image00493.jpeg)

Open, Software Manager

Type In,

discord

Click, Discord

Click, Install

Discord Install Using flatpak Command Line

![](Images/image00494.jpeg)

Open, Terminal

Type In,

flatpak install flathub com.discordapp.Discord

Press, Enter

Discord Install Using Snap Store

![](Images/image00495.jpeg)

Open, Snap Store

Type In,

discord

Click, Discord

Click, Install

Discord Install Using snap Command Line

![](Images/image00496.jpeg)

Open, Terminal

Type In,

sudo snap install discord

Press, Enter

Discord Install Using .deb

![](Images/image00497.jpeg)

Go to,

[https://discord.com/](https://discord.com/)

Click, Download for Linux

Click, deb to Download discord-0.0.18.deb

Go to, Where discord-0.0.18.deb is Downloaded.

Double Click, discord-0.0.18.deb

Click, Install

Ferdium

Ferdium Install Using Software Manager

![](Images/image00498.jpeg)

Open, Software Manager

Type In,

ferdium

Click, Ferdium

Click, Install

Ferdium Install Using flatpak Command Line

![](Images/image00499.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.ferdium.Ferdium

Press, Enter

Ferdium Install Using Snap Store

![](Images/image00500.jpeg)

Open, Snap Store

Type In,

ferdium

Click, ferdium

Click, Install

Ferdium Install Using snap Command Line

![](Images/image00501.jpeg)

Open, Terminal

Type In,

sudo snap install ferdium

Press, Enter

Ferdium Install Using .deb

![](Images/image00502.jpeg)

Go to,

[https://github.com/ferdium/ferdium-app/releases/tag/v6.0.0](https://github.com/ferdium/ferdium-app/releases/tag/v6.0.0)

Click,

Ferdium-linux-6.0.0-amd64.deb to Download

Ferdium-linux-6.0.0-amd64.deb

Go to, Where

Ferdium-linux-6.0.0-amd64.deb  is Downloaded

Double Click,

Ferdium-linux-6.0.0-amd64.deb

Click, Install

Pidgin

Pidgin Install Using Software Manager

![](Images/image00503.jpeg)

Open, Software Manager

Type In,

pidgin

Click, Pidgin

Click, Install

Pidgin Install Using apt Command Line

![](Images/image00504.jpeg)

Open, Terminal

Type In,

sudo apt install pidgin

Press, Enter

Pidgin Install Using flatpak Command Line

![](Images/image00505.jpeg)

Open, Terminal

Type In,

flatpak install flathub im.pidgin.Pidgin

Press, Enter

Signal

Signal Install Using Software Manager

![](Images/image00506.jpeg)

Open, Software Manager

Type In,

signal

Click, Signal Desktop

Click, Install

Signal Install Using flatpak Command Line

![](Images/image00507.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.signal.Signal

Press, Enter

Signal Install Using Snap Store

![](Images/image00508.jpeg)

Open, Snap Store

Type In,

signal

Click, signal-desktop

Click, Install

Signal Install Using snap Command Line

![](Images/image00509.jpeg)

Open, Terminal

Type In,

sudo snap install signal-desktop

Press, Enter

Telegram

Telegram Install Using Software Manager

![](Images/image00510.jpeg)

Open, Software Manager

Type In,

telegram

Click, Telegram

Click, Install

Telegram Install Using flatpak Command Line

![](Images/image00511.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.telegram.desktop

Press, Enter

Telegram Install Using Snap Store

![](Images/image00512.jpeg)

Open, Snap Store

Type In,

telegram

Click, telegram-desktop

Click, Install

Telegram Install Using snap Command Line

![](Images/image00513.jpeg)

Open, Terminal

Type In,

sudo snap install telegram-desktop

Press, Enter

Cryptocurrency Wallets

Cryptocurrency Wallets enable storage of crypto on Linux Operating Systems and offer,

*   Add-ons that raise features, e.g. trackers, email and virtual keyboard
*   Decentralized and redundant servers to lower downtime
*   Encryption and local storage of private keys which can be exported

This chapter covers,

Coin

*   Coin Install Using Snap Store
*   Coin Install Using snap Command Line

Exodus

*   Exodus Install Using Software Manager
*   Exodus Install Using flatpak Command Line
*   Exodus Install Using .deb

Guarda Wallet

*   Guarda Install Using .deb

Wasabi Wallet

*   Wasabi Wallet Install Using Software Manager
*   Wasabi Wallet Install Using flatpak Command Line
*   Wasabi Wallet Install Using .deb

Coin

Coin Install Using Snap Store

![](Images/image00514.jpeg)

Open, Snap Store

Type In,

coin

Click, Coin

Click, Install

Coin Install Using snap Command Line

![](Images/image00515.jpeg)

Open, Terminal

Type In,

sudo snap install coin

Press, Enter

Exodus

Exodus Install Using Software Manager

![](Images/image00516.jpeg)

Open, Software Manager

Type In,

exodus

Click, Exodus

Click, Install

Exodus Install Using flatpak Command Line

![](Images/image00517.jpeg)

Open, Terminal

Type In,

flatpak install flathub io.exodus.Exodus

Press, Enter

Exodus Install Using .deb

![](Images/image00518.jpeg)

Go to,

https://www.exodus.com/download/

Click, Download Exodus

Click, Download Linux app (.deb) to Download exodus-linux-x64-22.7.29.deb

Go to, Where exodus-linux-x64-22.7.29.deb is Downloaded

Double Click, exodus-linux-x64-22.7.29.deb

Click, Install

Guarda Wallet

Guarda Install Using .deb

![](Images/image00519.jpeg)

Go to,

[https://guarda.com/desktop/](https://guarda.com/desktop/)

Click, Download Guarda

Click, Download Linux (.deb) to Download Guarda_1.0.20_amd64.deb

Go to, Where Guarda_1.0.20_amd64.deb is Downloaded

Double Click, Guarda_1.0.20_amd64.deb

Click, Install

Wasabi Wallet

Wasabi Wallet Install Using Software Manager

![](Images/image00520.jpeg)

Open, Software Manager

Type In,

wasabi

Click, Wasabi Wallet

Click, Install

Wasabi Wallet Install Using flatpak Command Line

![](Images/image00521.jpeg)

Open, Terminal

Type In,

flatpak install flathub io.wasabiwallet.WasabiWallet

Press, Enter

Wasabi Wallet Install Using .deb

![](Images/image00522.jpeg)

Go to,

[https://wasabiwallet.io/index.html#download](https://wasabiwallet.io/index.html#download)

Click, Download under UBUNTU / DEBIAN to Download Wasabi-2.0.1.3.deb

Go to, Where Wasabi-2.0.1.3.deb is Downloaded

Double Click, Wasabi-2.0.1.3.deb

Click, Install

Custom Kernels

Custom kernels (for these purposes) are drop in replacements for the Linux Mint 21 5.15 Kernel, that offer additional features such as,

*   The latest kernel from 5.18.15 and above or later
*   Improvements to CPUFreq Governor, cache and virtual memory managers
*   Better framerates in World of Warcraft (from my experience)

This chapter covers,

Liquorix

*   Liquorix Install Using apt Command Line

Xanmod Stable

*   Xanmod Stable Install Using apt Command Line

Liquorix

Liquorix Install Using apt Command Line

![](Images/image00523.jpeg)

Open, Terminal

Type In,

sudo add-apt-repository ppa:damentz/liquorix && sudo apt-get update

Press, Enter

![](Images/image00524.jpeg)

Type In,

sudo apt-get install linux-image-liquorix-amd64 linux-headers-liquorix-amd64

Press, Enter

After Install, Restart, PC

Xanmod Stable

Xanmod Stable Install Using apt Command Line

![](Images/image00525.jpeg)

Open, Terminal

Type In,

echo 'deb http://deb.xanmod.org releases main' | sudo tee /etc/apt/sources.list.d/xanmod-kernel.list

Press, Enter

![](Images/image00526.jpeg)

Type In,

wget -qO - https://dl.xanmod.org/gpg.key | sudo apt-key --keyring /etc/apt/trusted.gpg.d/xanmod-kernel.gpg add -

Press, Enter

![](Images/image00527.jpeg)

Type In,

sudo apt update && sudo apt install linux-xanmod

Press, Enter

After Install, Restart PC

![](Images/image00528.jpeg)

If Using Intel CPU

Type In,

sudo apt install intel-microcode iucode-tool

Press, Enter

![](Images/image00529.jpeg)

Or If Using AMD CPU

Type In,

sudo apt install amd64-microcode

Press, Enter

![](Images/image00530.jpeg)

Type In,

echo 'net.core.default_qdisc = fq_pie' | sudo tee /etc/sysctl.d/90-override.conf

Press, Enter

Afterwards, Restart PC

Data Recovery

Data Recovery programs regain lost or damaged data from a storage device with features like,

*   Recognizing partition tables and layouts from various operating systems
*   Recover deleted variant of files using many parameters
*   SMART (Self-Monitoring, Analysis and Reporting Technology) to assess storage health

This chapter covers,

R-Linux

*   R-Linux Install Using .deb

R-Linux

R-Linux Install Using .deb

![](Images/image00531.jpeg)

Go to,

https://www.r-studio.com/free-linux-recovery/Download.shtml

Click, Download Now, In the same row as R-Linux for Debian/Ubuntu Linux platform (64-bit), to Download, RLinux5_x64.deb

Go to, Where RLinux5_x64.deb, is downloaded

Double Click, RLinux5_x64.deb

Click, Install

Desktop Environments

Desktop Environments are graphical user interfaces to access program and offer,

*   Drag and drop and additional features that make DE’s more familiar
*   Folders, icons, windows, wallpapers, toolbars and widgets
*   Gnome, KDE Plasma, Cinnamon and LXDE rank among the most popular DE’s

This chapter covers,

Tasksel

*   Tasksel Install Using apt Command Line

KDE Plasma

*   KDE Plasma Install Using apt Command Line

LXDE

*   LXDE Install Using apt Command Line

LXQT

*   LXQT Install Using apt Command Line

Gnome

*   Gnome Install Using tasksel Command Line

Tasksel

Tasksel Install Using apt Command Line

![](Images/image00532.jpeg)

Open, Terminal

Type In,

sudo apt install tasksel

Press, Enter

KDE Plasma

KDE Plasma Install Using apt Command Line

![](Images/image00533.jpeg)

Open, Terminal

Type In,

sudo apt install kde-full

Press, Enter

LXDE

LXDE Install Using apt Command Line

![](Images/image00534.jpeg)

Open, Terminal

Type In,

sudo apt install lxde

Press, Enter

LXQT

LXQT Install Using apt Command Line

![](Images/image00535.jpeg)

Open, Terminal

Type In,

sudo apt install lxqt

Press, Enter

Gnome

Gnome Install Using tasksel Command Line

![](Images/image00536.jpeg)

Open, Terminal

Type In,

sudo tasksel

Press, Enter

![](Images/image00537.jpeg)

Select, GNOME with UP and DOWN arrows

Press, Space

Select, OK with Tab

Press, Enter

Download Managers

Download Managers are software that downloads files from the internet with features like,

*   Bandwidth limiters to ensure operations do not reduce connection
*   Connection settings and profiles that can be adjusted for each website
*   Schedule downloads to begin and end at certain dates

This chapter covers,

FlareGet

*   FlareGet Install Using .deb

KGet

*   KGet Install Using Software Manager
*   KGet Install Using apt Command Line
*   KGet Install Using flatpak Command Line

Motrix

*   Motrix Install Using Snap Store
*   Motrix Install Using snap Command Line
*   Motrix Install Using .deb

Persepolis

*   Persepolis Install Using apt Command Line

uGet

*   uGet Install Using Software Manager
*   uGet Install Using apt Command Line

FlareGet

FlareGet Install Using .deb

![](Images/image00538.jpeg)

Go to,

https://flareget.com/download.html

Click, Download 64-bit under FlareGet 5.0-0 (Deb) to Download flareget_5.0-1_amd64.deb

Go to, Where flareget_5.0-1_amd64.deb is Downloaded

Double Click, flareget_5.0-1_amd64.deb

Click, Install

KGet

KGet Install Using Software Manager

![](Images/image00539.jpeg)

Open, Software Manager

Type In,

kget

Click, KGet

Click, Install

KGet Install Using apt Command Line

![](Images/image00540.jpeg)

Open, Terminal

Type In,

sudo apt install kget

Press, Enter

KGet Install Using flatpak Command Line

![](Images/image00541.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.kde.kget

Press, Enter

Motrix

Motrix Install Using Snap Store

![](Images/image00542.jpeg)

Open, Snap Store

Type In,

motrix

Click, Motrix

Click, Install

Motrix Install Using snap Command Line

![](Images/image00543.jpeg)

Open, Terminal

Type In,

sudo snap install motrix

Press, Enter

Motrix Install Using .deb

![](Images/image00544.jpeg)

Go to,

[https://github.com/agalwood/Motrix/releases/tag/v1.6.11](https://github.com/agalwood/Motrix/releases/tag/v1.6.11)

Click, Motrix_1.6.11_amd64.deb to Download Motrix_1.6.11_amd64.deb

Go to, Where Motrix_1.6.11_amd64.deb is downloaded

Double Click, Motrix_1.6.11_amd64.deb

Click, Install

Persepolis

Persepolis Install Using apt Command Line

![](Images/image00545.jpeg)

Open, Terminal

Type In,

sudo add-apt-repository ppa:persepolis/ppa && sudo apt update && sudo apt install persepolis

Press, Enter

uGet

uGet Install Using Software Manager

![](Images/image00546.jpeg)

Open, Software Manager

Type In,

uGet

Click, Uget

Click, Install

uGet Install Using apt Command Line

![](Images/image00547.jpeg)

Open, Terminal

Type In,

sudo apt install uget

Press, Enter

Ebook Readers

Ebook Readers are software that permits viewing of electronic books, with features such as,

*   Changing the font type and size to suit the readers persuasion
*   Convert ebooks between different formats to suit the readers needs
*   Fetching newsfeeds for easy viewing in an ebook format

This chapter covers,

Calibre

*   Calibre Install Using Software Manager
*   Calibre Install Using apt Command Line
*   Calibre Install Using flatpak Command Line
*   Calibre Install Using Binary install Command Line

FBReader

*   FBReader Install Using Software Manager
*   FBReader Install Using apt Command Line
*   FBReader Install Using Snap Store
*   FBReader Install Using snap Command Line

Lucidor

*   Lucidor Install Using .deb

Okular

*   Okular Install Using Software Manager
*   Okular Install Using apt Command Line
*   Okular Install Using flatpak Command Line
*   Okular Install Using Snap Store
*   Okular Install Using snap Command Line

Bookworm

*   Bookworm Install Using Software Manager
*   Bookworm Install Using apt Command Line
*   Bookworm Install Using flatpak Command Line

Calibre

Calibre Install Using Software Manager

![](Images/image00548.jpeg)

Open, Software Manager

Type In,

calibre

Click, calibre

Click, Install

Calibre Install Using apt Command Line

![](Images/image00549.jpeg)

Open, Terminal

Type In,

sudo apt install calibre

Press, Enter

Calibre Install Using flatpak Command Line

![](Images/image00550.jpeg)

Open, Terminal

Type In,

flatpak install flathub com.calibre_ebook.calibre

Press, Enter

Calibre Install Using Binary install Command Line

![](Images/image00551.jpeg)

Open, Terminal

Type In,

sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin

Press, Enter

FBReader

FBReader Install Using Software Manager

![](Images/image00552.jpeg)

Open, Software Manager

Type In,

fbreader

Click, E-book reader

Click, Install

FBReader Install Using apt Command Line

![](Images/image00553.jpeg)

Open, Terminal

Type In,

sudo apt install fbreader

Press, Enter

FBReader Install Using Snap Store

![](Images/image00554.jpeg)

Open, Snap Store

Type In,

fbreader

Click, FBReader 2.0

Click, Install

FBReader Install Using snap Command Line

![](Images/image00555.jpeg)

Open, Terminal

Type In,

sudo snap install fbreader

Press, Enter

Lucidor

Lucidor Install Using .deb

![](Images/image00556.jpeg)

Go to,

http://lucidor.org/lucidor/download.php

Click, Download the deb package: lucidor_0.9.15-1_all.deb to Download lucidor_0.9.15-1_all.deb

Go to, Where lucidor_0.9.15-1_all.deb is downloaded

Double Click, lucidor_0.9.15-1_all.deb

Click, Install

Okular

Okular Install Using Software Manager

![](Images/image00557.jpeg)

Open, Software Manager

Type In,

okular

Click, Okular

Click, Install

Okular Install Using apt Command Line

![](Images/image00558.jpeg)

Open, Terminal

Type In,

sudo apt install okular

Press, Enter

Okular Install Using flatpak Command Line

![](Images/image00559.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.kde.okular

Press, Enter

Okular Install Using Snap Store

![](Images/image00560.jpeg)

Open, Snap Store

Type In,

okular

Click, Okular

Click, Install

Okular Install Using snap Command Line

![](Images/image00561.jpeg)

Open, Terminal

Type In,

sudo snap install okular

Press, Enter

Bookworm

Bookworm Install Using Software Manager

![](Images/image00562.jpeg)

Open, Software Manager

Type In,

bookworm

Click, Bookworm

Click, Install

Bookworm Install Using apt Command Line

![](Images/image00563.jpeg)

Open, Terminal

Type In,

sudo apt install bookworm

Press, Enter

Bookworm Install Using flatpak Command Line

![](Images/image00564.jpeg)

Open, Terminal

Type In,

flatpak install flathub com.github.babluboy.bookworm

Press, Enter

Elder Gaming

Elder Gaming is about running elder games on linux operating systems, with tools like,

*   DOSBox lets games made for dos run on other OS’s
*   ResidualVM is about playing 3d adventure games unsupported by ScummVM
*   ScummVM runs elder adventure games with features like save states

This chapter covers,

DOSBox

*   DOSBox Install Using Software Manager
*   DOSBox Install Using apt Command Line
*   DOSBox Install Using flatpak Command Line
*   libopusfile0 Install Using apt Command Line

Gnome Games App

*   Gnome Games App Install Using Software Manager
*   Gnome Games App Install Using apt Command Line
*   Gnome Games App Install Using flatpak Command Line

ScummVM

*   ScummVM Install Using Software Manager
*   ScummVM Install Using apt Command Line
*   ScummVM Install Using flatpak Command Line
*   ScummVM Install Using Snap Store
*   ScummVM Install Using snap Command Line

DOSBox

DOSBox Install Using Software Manager

![](Images/image00565.jpeg)

Open, Software Manger

Type In,

dosbox

Click, DOSBox

Click, Install

DOSBox Install Using apt Command Line

![](Images/image00566.jpeg)

Open, Terminal

Type In,

sudo apt install dosbox

Press, Enter

DOSBox Install Using flatpak Command Line

![](Images/image00567.jpeg)

Open, Terminal

Type In,

flatpak install flathub com.dosbox.DOSBox

Press, Enter

libopusfile0 Install Using apt Command Line

![](Images/image00568.jpeg)

Open, Terminal

Type In,

sudo apt install libopusfile0

Press, Enter

Gnome Games App

Gnome Games App Install Using Software Manager

![](Images/image00569.jpeg)

Open, Software Manager

Type In,

gnome games

Click, Games

Click, Install

Gnome Games App Install Using apt Command Line

![](Images/image00570.jpeg)

Open, Terminal

Type In,

sudo apt install gnome-games-app

Press, Enter

Gnome Games App Install Using flatpak Command Line

![](Images/image00571.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.gnome.Games

Press, Enter

ScummVM

ScummVM Install Using Software Manager

![](Images/image00572.jpeg)

Open, Software Manager

Type In,

scummvm

Click, ScummVM

Click, Install

ScummVM Install Using apt Command Line

![](Images/image00573.jpeg)

Open, Terminal

Type In,

sudo apt install scummvm

Press, Enter

ScummVM Install Using flatpak Command Line

![](Images/image00574.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.scummvm.ScummVM

Press, Enter

ScummVM Install Using Snap Store

![](Images/image00575.jpeg)

Open, Snap Store

Type In,

scummvm

Click, ScummVM

Click, Install

ScummVM Install Using snap Command Line

![](Images/image00576.jpeg)

Open, Terminal

Type In,

sudo snap install scummvm

Press, Enter

File Compression and Extraction

File Compression and Extraction software that compress and extracts files, with added bits like,

*   Encrypting folders with industry leading standards
*   Extracting files into a new folder based on file names
*   Finding balance around compression ratio and task completion speed

This chapter covers,

P7Zip-Desktop

*   P7Zip-Desktop Install Using Snap Store
*   P7Zip-Desktop Install Using snap Command Line

Peazip

*   Peazip Install Using Software Manager
*   Peazip Install Using flatpak Command Line
*   Peazip Install Using .deb

P7Zip-Desktop

P7Zip-Desktop Install Using Snap Store

![](Images/image00577.jpeg)

Open, Snap Store

Type In,

p7zip-desktop

Click, p7zip-desktop

Click, Install

P7Zip-Desktop Install Using snap Command Line

![](Images/image00578.jpeg)

Open, Terminal

Type In,

sudo snap install p7zip-desktop

Press, Enter

Peazip

Peazip Install Using Software Manager

![](Images/image00579.jpeg)

Open, Software Manager

Type In,

peazip

Click, Peazip

Click, Install

Peazip Install Using flatpak Command Line

![](Images/image00580.jpeg)

Open, Terminal

Type In,

flatpak install flathub io.github.peazip.PeaZip

Press, Enter

Peazip Install Using .deb

![](Images/image00581.jpeg)

Go to,

https://peazip.github.io/peazip-linux.html

Click, DEB GTK2 to Download peazip_8.7.0.LINUX.GTK2-1_amd64.deb

Go to, Where peazip_8.7.0.LINUX.GTK2-1_amd64.deb is Downloaded

Double Click, peazip_8.7.0.LINUX.GTK2-1_amd64.deb

Click, Install

Firewall

Firewall programs help protect computers from malicious actors conducting external attacks, and include,

*   Easy to use and readily accessible graphical interface
*   Choice of simple or more advanced configuration options
*   Open only the ports the user requires for their software

This chapter covers,

All The Firewall Rules I Use

*   TCP Ports
*   UDP Ports

UFW

*   UFW Install Using apt Command Line
*   UFW Enable
*   UFW Add Single Port Rule
*   UFW Add Multi Port Rule
*   UFW Add Range Port Rule
*   UFW Remove Port Rule

Firewall Configuration

*   Firewall Configuration Install Using Software Manager
*   Firewall Configuration Install Using apt Command Line
*   Firewall Configuration Add Single Port Rule
*   Firewall Configuration Add Multi Port Rule
*   Firewall Configuration Add Range Port Rule
*   Firewall Configuration Add Rule From Report
*   Firewall Configuration Remove Firewall Rule

All The Firewall Rules I Use

TCP Ports

53,80,433,443,1119,1120,1716,1935,2099,3074,3075,3216,3478,3479,3569,3724,4000,5060,5062,5222,5223,6012,6112,6113,6114,6250,8080,8088,8094,8097,9946,9988,14000,14008,14020,14021,14022,14023,14024,17502,17503,17504,18000,18060,18120,22990,27900,29810,29900,42124,42125,42126,42127,42130,20000:20100,25000:25099,27014:27050,30000:30099,42100:42200,6112:6119,6113:6119,7777:7780,8393:8400,9960:9969  

UDP Ports

67,68,80,443,546,631,1119,1120,1716,3074,3126,3478,3659,3724,4000,4000,5060,5062,6012,6112,6113,6114,6120,6250,8080,8088,8125,9565,9570,18000,27036,29900,10000:19999,1024:1124,1119:1120,12000:64000,14000:14016,21000:26000,22990:23006,25000:25099,25200:25300,27000:27031,30000:30099,3074:3083,3478:3479,37000:39999,37000:40000,4379:4380,5000:5500,6112:6119,9000:9999

UFW

UFW Install Using apt Command Line

![](Images/image00582.jpeg)

Open, Terminal

Type In,

sudo apt install ufw

Press, Enter

UFW Enable

![](Images/image00583.jpeg)

Open, Terminal

Type In,

sudo ufw enable

Press, Enter

UFW Add Single Port Rule

![](Images/image00584.jpeg)

Open, Terminal

Type In,

sudo ufw allow 80/tcp

or

sudo ufw allow 80/udp

Press, Enter

UFW Add Multi Port Rule

![](Images/image00585.jpeg)

Open, Terminal

Type In,

sudo ufw allow 80,443/tcp

or

sudo ufw allow 80,443/udp

Press, Enter

UFW Add Range Port Rule

![](Images/image00586.jpeg)

Open, Terminal

Type In,

sudo ufw allow 1119:1120/tcp

or

sudo ufw allow 1119:1120/udp

Press, Enter

UFW Remove Port Rule

![](Images/image00587.jpeg)

Open, Terminal

Type In,

sudo ufw status numbered

Press, Enter

![](Images/image00588.jpeg)

Choose rule to delete and make note of the rule number

Type In,

sudo ufw delete 224

Press, Enter

Firewall Configuration

Firewall Configuration Install Using Software Manager

![](Images/image00589.jpeg)

Open , Software Manager

Type In,

gufw

Click, Firewall Configuration

Click, Install

Firewall Configuration Install Using apt Command Line

![](Images/image00590.jpeg)

Open, Terminal

Type In,

sudo apt install gufw

Press, Enter

Firewall Configuration Add Single Port Rule

![](Images/image00591.jpeg)

Open, Firewall Configuration

Click, Rules

Click, +

Click, Simple

Click, Box in the same row as Name

Type In,

HTTP

Click, Box in the same row as Direction

Click, In

Click, Box In the same row as Protocol

Click, TCP, UDP or Both

Click, Box in the same row as Port

Type In,

80

Click, Add

Firewall Configuration Add Multi Port Rule

![](Images/image00592.jpeg)

Open, Firewall Configuration

Click, Rules

Click, +

Click, Simple

Click, Box in the same row as Name

Type In,

Multi Port Rule 1

Click, Box in the same row as Direction

Click, In

Click, Box in the same row as Protocol

Click, TCP, UDP or Both

Click, Box in the same row as Port

Type In, 80,443

Click, Add

Firewall Configuration Add Range Port Rule

![](Images/image00593.jpeg)

Open, Firewall Configuration

Click, Rules

Click, +

Click, Simple

Click, Box in the same row as Name

Type In,

Range Port Rule 1

Click, Box in the same row as Direction

Click, In

Click, Box in the same row as Protocol

Click, TCP, UDP or Both

Click, Box in the same row as Port

Type In,

1119:1120

Click, Add

Firewall Configuration Add Rule From Report

![](Images/image00594.jpeg)

Open, Firewall Configuration

Click, Report

Select, Row from report

Click, +

Click, Add

Firewall Configuration Remove Port Rule

![](Images/image00595.jpeg)

Open, Firewall Configuration

Click, Rules

Select, 224

Click, -

Game Engines

Games Engines are used by individuals and organizations to create games for Linux/Windows/Mac/Others, with notable examples being,

*   Godot
*   Spring Engine
*   Unity

This chapter covers,

Spring Engine

*   Spring Engine Install Using Snap Store
*   Spring Engine Install Using snap Command Line

Unity

*   Unity Install Using apt Command Line

Spring Engine

Spring Engine Install Using Snap Store

![](Images/image00596.jpeg)

Open, Snap Store

Type In,

springrts

Click, SpringLobby(nsg)

Click, Install

Spring Engine Install Using snap Command Line

![](Images/image00597.jpeg)

Open, Terminal

Type In,

sudo snap install springlobby-nsg

Press, Enter

Unity

Unity Install Using apt Command Line

![](Images/image00598.jpeg)

Open, Terminal

Type In,

sudo sh -c 'echo "deb https://hub.unity3d.com/linux/repos/deb stable main" > /etc/apt/sources.list.d/unityhub.list'

Press, Enter

![](Images/image00599.jpeg)

Type In,

wget -qO - https://hub.unity3d.com/linux/keys/public | sudo apt-key add -

Press, Enter

![](Images/image00600.jpeg)

Type In,

sudo apt update && sudo apt install unityhub

Press, Enter

Home Living 

Home Living is about software that improves or adds new dimensions to Home Life and example are,

*   Home Brewing to make your own drinks
*   Recipes to make the best of the ingredients at hand
*   Managing personal and household finances

This chapter covers,

AnyMeal

*   AnyMeal Install Using Software Manager
*   AnyMeal Install Using apt Command Line
*   AnyMeal Install Using .AppImage

GnuCash

*   GnuCash Install Using Software Manager
*   GnuCash Install Using apt Command Line
*   GnuCash Install Using flatpak Command Line

Gnome Recipes

*   Gnome Recipies Install Using Software Manager
*   Gnome Recipies Install Using apt Command Line
*   Gnome Recipies Install Using flatpak Command Line

Home Assistant

*   Home Assistant Install Using Snap Store
*   Home Assistant Install Using snap Command Line

HomeBank

*   HomeBank Install Using Software Manager
*   HomeBank Install Using apt Command Line
*   HomeBank Install Using flatpak Command Line

Skrooge

*   Skrooge Install Using Software Manager
*   Skrooge Install Using apt Command Line
*   Skrooge Install Using flatpak Command Line

Sweet Home 3D

*   Sweet Home 3D Install Using Software Manager
*   Sweet Home 3D Install Using apt Command Line
*   Sweet Home 3D Install Using Snap Store
*   Sweet Home 3D Install Using snap Command Line

AnyMeal

AnyMeal Install Using Software Manager

![](Images/image00601.jpeg)

Open, Software Manager

Type In,

anymeal

Click, AnyMeal recipe management software

Click, Install

AnyMeal Install Using apt Command Line

![](Images/image00602.jpeg)

Open, Terminal

Type In,

sudo apt install anymeal

Press, Enter

AnyMeal Install Using .AppImage

![](Images/image00602.jpeg)

Go to,

https://github.com/wedesoft/anymeal/releases/tag/v1.17

Click,

anymeal-f650986-x86_64.AppImage to Download

anymeal-f650986-x86_64.AppImage

Go to, Where

anymeal-f650986-x86_64.AppImage is Downloaded

Double Click,

anymeal-f650986-x86_64.AppImage

Click, Integrate and Run

GnuCash

GnuCash Install Using Software Manager

![](Images/image00603.jpeg)

Open, Software Manager

Type In,

gnucash

Click, GnuCash

Click, Install

GnuCash Install Using apt Command Line

![](Images/image00604.jpeg)

Open, Terminal

Type In,

sudo apt install gnucash

Press, Enter

GnuCash Install Using flatpak Command Line

![](Images/image00605.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.gnucash.GnuCash

Press, Enter

Gnome Recipes

Gnome Recipes Install Using Software Manager

![](Images/image00606.jpeg)

Open, Software Manager

Type In,

gnome recipes

Click, Recipes

Click, Install

Gnome Recipes Install Using apt Command Line

![](Images/image00607.jpeg)

Open, Terminal

Type In,

sudo apt install gnome-recipes

Press, Enter

Gnome Recipes Install Using flatpak Command Line

![](Images/image00608.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.gnome.Recipes

Press, Enter

Home Assistant

Home Assistant Install Using Snap Store

![](Images/image00609.jpeg)

Open, Snap Store

Type In,

home assistant

Click, Home Assistant

Click, Install

Home Assistant Install Using snap Command Line

![](Images/image00610.jpeg)

Open, Terminal

Type In,

sudo snap install home-assistant-snap

Press, Enter

HomeBank

HomeBank Install Using Software Manager

![](Images/image00611.jpeg)

Open, Software Manager

Type In,

homebank

Click, HomeBank

Click, Install

HomeBank Install Using apt Command Line

![](Images/image00612.jpeg)

Open, Terminal

Type In,

sudo apt install homebank

Press, Enter

HomeBank Install Using flatpak Command Line

![](Images/image00613.jpeg)

Open, Terminal

Type In,

flatpak install flathub fr.free.Homebank

Press, Enter

Skrooge

Skrooge Install Using Software Manager

![](Images/image00614.jpeg)

Open, Software Manager

Type In,

skrooge

Click, Skrooge

Click, Install

Skrooge Install Using apt Command Line

![](Images/image00614.jpeg)

Open, Terminal

Type In,

sudo apt install skrooge

Press, Enter

Skrooge Install Using flatpak Command Line

![](Images/image00615.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.kde.skrooge

Press, Enter

Sweet Home 3D

Sweet Home 3D Install Using Software Manager

![](Images/image00616.jpeg)

Open, Software Manager

Type In,

sweet home 3d

Click, Sweet Home 3D

Click, Install

Sweet Home 3D Install Using apt Command Line

![](Images/image00617.jpeg)

Open, Terminal

Type In,

sudo apt install sweethome3d

Press, Enter

Sweet Home 3D Install Using Snap Store

![](Images/image00618.jpeg)

Open, Snap Store

Type In,

sweet home 3d

Click, Sweet Home 3D

Click, Install

Sweet Home 3D Install Using snap Command Line

![](Images/image00619.jpeg)

Open, Terminal

Type In,

sudo snap install sweethome3d-homedesign

Press, Enter

Image Editors

Image Editors allow creation and editing of pictures, with features like,

*   Make blank canvases of all sizes and types to paint
*   Tremendous amount of painting tools that let images be fully customized
*   Wide variety of selection tools that let any part of the image be chosen

This chapter covers,

Blender

*   Blender Install Using Software Manager
*   Blender Install Using apt Command Line
*   Blender Install Using flatpak Command Line
*   Blender Install Using Snap Store
*   Blender Install Using snap Command Line

Gnu Image Manipulation Program

*   Gnu Image Manipulation Program Install Using Software Manager
*   Gnu Image Manipulation Program Install Using apt Command Line
*   Gnu Image Manipulation Program Install Using flatpak Command Line
*   Gnu Image Manipulation Program Install Using Snap Store
*   Gnu Image Manipulation Program Install Using snap Command Line

Inkscape

*   Inkscape Install Using Software Manager
*   Inkscape Install Using apt Command Line
*   Inkscape Install Using flatpak Command Line
*   Inkscape Install Using Snap Store
*   Inkscape Install Using snap Command Line

Krita

*   Krita Install Using Software Manager
*   Krita Install Using apt Command Line
*   Krita Install Using flatpak Command Line
*   Krita Install Using Snap Store
*   Krita Install Using snap Command Line

Pinta

*   Pinta Install Using Software Manager
*   Pinta Install Using apt Command Line
*   Pinta Install Using flatpak Command Line
*   Pinta Install Using Snap Store
*   Pinta Install Using snap Command Line

Blender

Blender Install Using Software Manager

![](Images/image00620.jpeg)

Open, Software Manager

Type In,

blender

Click, Blender

Click, Install

Blender Install Using apt Command Line

![](Images/image00621.jpeg)

Open, Terminal

Type In,

sudo apt install blender

Press, Enter

Blender Install Using flatpak Command Line

![](Images/image00622.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.blender.Blender

Press, Enter

Blender Install Using Snap Store

![](Images/image00623.jpeg)

Open, Snap Store

Type In,

blender

Click, blender

Click, Install

Blender Install Using snap Command Line

![](Images/image00624.jpeg)

Open, Terminal

Type In,

sudo snap install blender

Press, Enter

Gnu Image Manipulation Program

Gnu Image Manipulation Program Install Using Software Manager

![](Images/image00625.jpeg)

Open, Software Manager

Type In,

gnu image manipulation program

Click, GNU Image Manipulation Program

Click, Install

Gnu Image Manipulation Program Install Using apt Command Line

![](Images/image00626.jpeg)

Open, Terminal

Type In,

sudo apt install gimp

Press, Enter

Gnu Image Manipulation Program Install Using flatpak Command Line

![](Images/image00627.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.gimp.GIMP

Press, Enter

Gnu Image Manipulation Program Install Using Snap Store

![](Images/image00628.jpeg)

Open, Snap Store

Type In,

gnu image manipulation program

Click, Gnu Image Manipulation Program

Click, Install

Gnu Image Manipulation Program Install Using snap Command Line

![](Images/image00629.jpeg)

Open, Terminal

Type In,

sudo snap install gimp

Press, Enter

Inkscape

Inkscape Install Using Software Manager

![](Images/image00630.jpeg)

Open, Software Manager

Type In,

inkscape

Click, Inkscape

Click, Install

Inkscape Install Using apt Command Line

![](Images/image00631.jpeg)

Open, Terminal

Type In,

sudo apt install inkscape

Press, Enter

Inkscape Install Using flatpak Command Line

![](Images/image00632.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.inkscape.Inkscape

Press, Enter

Inkscape Install Using Snap Store

![](Images/image00633.jpeg)

Open, Snap Store

Type In,

inkscape

Click, inkscape

Click, Install

Inkscape Install Using snap Command Line

![](Images/image00634.jpeg)

Open, Terminal

Type In,

sudo snap install inkscape

Press, Enter

Krita

Krita Install Using Software Manager

![](Images/image00635.jpeg)

Open, Software Manager

Type In,

krita

Click, Krita

Click, Install

Krita Install Using apt Command Line

![](Images/image00636.jpeg)

Open, Terminal

Type In,

sudo apt install krita

Press, Enter

Krita Install Using flatpak Command Line

![](Images/image00637.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.kde.krita

Press, Enter

Krita Install Using Snap Store

![](Images/image00638.jpeg)

Open, Snap Store

Type In,

krita

Click, krita

Click, Install

Krita Install Using snap Command Line

![](Images/image00639.jpeg)

Open, Terminal

Type In,

sudo snap install krita

Click, Enter

Pinta

Pinta Install Using Software Manager

![](Images/image00640.jpeg)

Open, Software Manager

Type In,

pinta

Click, Pinta

Click, Install

Pinta Install Using apt Command Line

![](Images/image00641.jpeg)

Open, Terminal

Type In,

sudo apt install pinta

Press, Enter

Pinta Install Using flatpak Command Line

![](Images/image00642.jpeg)

Open, Terminal

Type In,

flatpak install flathub com.github.PintaProject.Pinta

Press, Enter

Pinta Install Using Snap Store

![](Images/image00643.jpeg)

Open, Snap Store

Type In,

pinta

Click, pinta

Click, Install

Pinta Install Using snap Command Line

![](Images/image00644.jpeg)

Open, Terminal

Type In,

sudo snap install pinta

Press, Enter

Integrated Development Environment

Intergrated Development Environment’s or IDE’s let beings code in one or a variety of languages, within it or their’s confines, with features like,

*   Java desktop, Web Applications, HTML5
*   Increasing functionality with 1st or 3rd party extensions
*   Looking over and debugging code, with reporting

This chapter covers,

Atom

*   Atom Install Using Software Manager
*   Atom Install Using flatpak Command Line
*   Atom Install Using .deb

Apache NetBeans

*   Apache NetBeans Install Using Software Manager
*   Apache NetBeans Install Using flatpak Command Line
*   Apache NetBeans Install Using Snap Store
*   Apache NetBeans Install Using snap Command Line

Bluefish Editor

*   Bluefish Editor Install Using Software Manager
*   Bluefish Editor Install Using apt Command Line
*   Bluefish Editor Install Using flatpak Command Line

Codium

*   Codium Install Using Snap Store
*   Codium Install Using snap Command Line

Eclipse

*   Eclipse Install Using Software Manager
*   Eclipse Install Using flatpak Command Line
*   Ecipse Install Using Snap Store
*   Eclipse Install Using snap Command Line

GNU Emacs

*   GNU Emacs Install Using Software Manager
*   GNU Emacs Install Using apt Command Line
*   GNU Emacs Install Using flatpak Command Line

Visual Studio Code

*   Visual Studio Code Install Using Software Manager
*   Visual Studio Code Install Using flatpak Command Line
*   Visual Studio Code Install Using Snap Store
*   Visual Studio Code Install Using snap Command Line

Atom

Atom Install Using Software Manager

![](Images/image00645.jpeg)

Open, Software Manager

Type In,

atom

Click, Atom

Click, Install

Atom Install Using flatpak Command Line

![](Images/image00646.jpeg)

Open, Terminal

Type In,

flatpak install flathub io.atom.Atom

Press, Enter

Atom Install Using .deb

![](Images/image00647.jpeg)

Go to,

[https://github.com/atom/atom/releases/tag/v1.60.0](https://github.com/atom/atom/releases/tag/v1.60.0)

Click, atom-amd64.deb to Download atom-amd64.deb

Go to, Where atom-amd64.deb is Downloaded

Double Click, atom-amd64.deb

Click, Install

Apache NetBeans

Apache NetBeans Install Using Software Manager

![](Images/image00648.jpeg)

Open, Software Manager

Type In,

netbeans

Click, NetBeans

Click, Install

Apache NetBeans Install Using flatpak Command Line

![](Images/image00649.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.apache.netbeans

Press, Enter

Apache NetBeans Install Using Snap Store

![](Images/image00650.jpeg)

Open, Snap Store

Type In,

netbeans

Click, Apache NetBeans

Click, Install

Apache NetBeans Install Using snap Command Line

![](Images/image00651.jpeg)

Open, Terminal

Type In,

sudo snap install netbeans

Press, Enter

Bluefish Editor

Bluefish Editor Install Using Software Manager

![](Images/image00652.jpeg)

Open, Software Manager

Type In,

bluefish

Click, Bluefish Editor

Click, Install

Bluefish Editor Install Using apt Command Line

![](Images/image00653.jpeg)

Open, Terminal

Type In,

sudo apt install bluefish

Press, Enter

Bluefish Editor Install Using flatpak Command Line

![](Images/image00654.jpeg)

Open, Terminal

Type In,

flatpak install flathub nl.openoffice.bluefish

Press, Enter

Codium

Codium Install Using Snap Store

![](Images/image00655.jpeg)

Open, Snap Store

Type In,

codium

Click, codium

Click, Install

Codium Install Using snap Command Line

![](Images/image00656.jpeg)

Open, Terminal

Type In,

sudo snap install codium

Press, Enter

Eclipse

Eclipse Install Using Software Manager

![](Images/image00657.jpeg)

Open, Software Manager

Type In,

eclipse

Click, Eclipse IDE for Java Developers

Click, Download

Eclipse Install Using flatpak Command Line

![](Images/image00658.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.eclipse.Java

Press, Enter

Ecipse Install Using Snap Store

![](Images/image00659.jpeg)

Open, Snap Store

Type In,

eclipse

Click, Eclipse

Click, Install

Eclipse Install Using snap Command Line

![](Images/image00660.jpeg)

Open, Terminal

Type In,

sudo snap install eclipse

Press, Enter

GNU Emacs

GNU Emacs Install Using Software Manager

![](Images/image00661.jpeg)

Open, Software Manager

Type In,

emacs

Click, Emacs (GUI)

Click, Install

GNU Emacs Install Using apt Command Line

![](Images/image00662.jpeg)

Open, Terminal

Type In,

sudo apt install emacs

Press, Enter

GNU Emacs Install Using flatpak Command Line

![](Images/image00663.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.gnu.emacs

Press, Enter

Visual Studio Code

Visual Studio Code Install Using Software Manager

![](Images/image00664.jpeg)

Open, Software Manager

Type In,

visual studio code

Click, Visual Studio Code

Click, Install

Visual Studio Code Install Using flatpak Command Line

![](Images/image00665.jpeg)

Open, Terminal

Type In,

flatpak install flathub com.visualstudio.code

Press, Enter

Visual Studio Code Install Using Snap Store

![](Images/image00666.jpeg)

Open, Snap Store

Type In,

visual studio code

Click, code

Click, Install

Visual Studio Code Install Using snap Command Line

![](Images/image00667.jpeg)

Open, Terminal

Type In,

sudo snap install code

Press, Enter

Media Players

Media Players are programs which play a variety of media files, with added options,

*   Add effects and filters to change the way media is played
*   Create and rearrange playlists manually or automatically
*   Play, pause, rewind , fast forward or skip to previous or next media

This chapter covers

Haruna

*   Haruna Install Using Software Manager
*   Haruna Install Using flatpak Command Line

Parole

*   Parole Install Using Software Manager
*   Parole Install Using apt Command Line

SMPlayer

*   SMPlayer Install Using Software Manager
*   SMPlayer Install Using apt Command Line
*   SMPlayer Install Using flatpak Command Line
*   SMPlayer Install Using Snap Store
*   SMPlayer Install Using snap Command Line

VLC

*   VLC Install Using Software Manager
*   VLC Install Using apt Command Line
*   VLC Install Using flatpak Command Line

Haruna

Haruna Install Using Software Manager

![](Images/image00668.jpeg)

Open, Software Manager

Type In,

haruna

Click, Haruna

Click, Install

Haruna Install Using flatpak Command Line

![](Images/image00669.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.kde.haruna

Press, Enter

Parole

Parole Install Using Software Manager

![](Images/image00670.jpeg)

Open, Software Manager

Type In,

parole

Click, Parole

Click, Install

Parole Install Using apt Command Line

![](Images/image00671.jpeg)

Open, Terminal

Type In,

sudo apt install parole

Press, Enter

SMPlayer

SMPlayer Install Using Software Manager

![](Images/image00672.jpeg)

Open, Software Manager

Type In,

smplayer

Click, SMPlayer

Click, Install

SMPlayer Install Using apt Command Line

![](Images/image00673.jpeg)

Open, Terminal

Type In,

sudo apt install smplayer

Press, Enter

SMPlayer Install Using flatpak Command Line

![](Images/image00674.jpeg)

Open, Terminal

Type In,

flatpak install flathub info.smplayer.SMPlayer

Press, Enter

SMPlayer Install Using Snap Store

![](Images/image00675.jpeg)

Open, Snap Store

Type In,

smplayer

Click, smplayer

Click, Install

SMPlayer Install Using snap Command Line

![](Images/image00676.jpeg)

Open, Terminal

Type In,

sudo snap install smplayer

Press, Enter

VLC

VLC Install Using Software Manager

![](Images/image00677.jpeg)

Open, Software Manager

Type In,

vlc

Click, VLC

Click, Install

VLC Install Using apt Command Line

![](Images/image00678.jpeg)

Open, Terminal

Type In,

sudo apt install vlc

Press, Enter

VLC Install Using flatpak Command Line

![](Images/image00679.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.videolan.VLC

Press, Enter

Modern Gaming

Modern Gaming is dedicated to playing modern games on Linux Operating Systems, featuring,

*   KDE Games offering a wide variety of desktop fun
*   Lutris making it easier than ever before to play World of Warcraft
*   Steam granting access to the largest digital gaming store front

This chapter covers,

WINE

*   WINE Staging Install Using apt Command Line

Lutris

*   Lutris Install Using Software Manager
*   Lutris Install Using apt Command Line
*   Lutris Install Using Repository and apt Command Line

Steam

*   Steam Install Using Software Manager
*   Steam Install Using apt Command Line
*   Steam Install Using Snap Store
*   Steam Install Using snap Command Line

ProtonUp-Qt

*   ProtonUp-Qt Install Using Software Manager
*   ProtonUp-Qt Install Using flatpak Command Line
*   ProtonUp-Qt Install Using .AppImage

Proton-GE

*   Proton-GE Lutris Install Using .tar.gz
*   Proton-GE Steam Install Using .tar.gz

WINE-GE

*   WINE-GE Lutris Install Using .tar.xz

DXVK

*   DXVK Install Using .sh Command Line

VKD3D

*   VKD3D Install Using .sh Command Line

Gnome Games

*   Gnome Games Install Using apt Command Line

KDE Games

*   KDE Games Install Using apt Command Line

Gamehub

*   Gamehub Install Using Software Manager
*   Gamehub Install Using flatpak Command Line

WINE

WINE Staging Install Using apt Command Line

![](Images/image00680.jpeg)

Open, Terminal

Type In,

sudo dpkg --add-architecture i386 && sudo apt update

Press, Enter

![](Images/image00681.jpeg)

Type In,

wget -nc https://dl.winehq.org/wine-builds/ubuntu/dists/jammy/winehq-jammy.sources

Press, Enter

![](Images/image00682.jpeg)

Type In,

sudo mv winehq-jammy.sources /etc/apt/sources.list.d/

Press, Enter

![](Images/image00683.jpeg)

Type In,

wget -nc https://dl.winehq.org/wine-builds/winehq.key

Press, Enter

![](Images/image00684.jpeg)

Type In,

sudo mv winehq.key /usr/share/keyrings/winehq-archive.key

Press, Enter

![](Images/image00685.jpeg)

Type In,

sudo apt update

Press, Enter

![](Images/image00686.jpeg)

Type In,

sudo apt install --install-recommends winehq-staging

Press, Enter

Lutris

Lutris Install Using Software Manager

![](Images/image00687.jpeg)

Open, Software Manager

Type In,

lutris

Click, Lutris

Click, Install

Lutris Install Using apt Command Line

![](Images/image00688.jpeg)

Open, Terminal

Type In,

sudo apt install lutris

Press, Enter

Lutris Install Using Repository and apt Command Line

![](Images/image00689.jpeg)

Open, Terminal

Type In,

sudo add-apt-repository ppa:lutris-team/lutris && sudo apt update && sudo apt install lutris && sudo apt install winbind

Press, Enter

Steam

Steam Install Using Software Manager

![](Images/image00690.jpeg)

Open, Software Manager

Type In,

steam

Click, Steam installer

Click, Install

Steam Install Using apt Command Line

![](Images/image00691.jpeg)

Open, Terminal

Type In,

sudo apt install steam

Press, Enter

Steam Install Using Snap Store

![](Images/image00692.jpeg)

Open, Snap Store

Type In,

steam

Click, Steam

Click, Install

Steam Install Using snap Command Line

![](Images/image00693.jpeg)

Open, Terminal

Type In,

sudo snap install steam

Press, Enter

ProtonUp-Qt

ProtonUp-Qt Install Using Software Manager

![](Images/image00694.jpeg)

Open, Software Manager

Type In,

protonup-qt

Click, ProtonUp-Qt

Click, Install

ProtonUp-Qt Install Using flatpak Command Line

![](Images/image00695.jpeg)

Open, Terminal

Type In,

flatpak install flathub net.davidotek.pupgui2

Press, Enter

ProtonUp-Qt Install Using .AppImage

![](Images/image00696.jpeg)

Go to,

https://davidotek.github.io/protonup-qt/

Click, ProtonUp-Qt

Click, Download ProtonUp-Qt v2.6.5 to Download ProtonUp-Qt-2.6.5-x86_64.AppImage

Go to, Where ProtonUp-Qt-2.6.5-x86_64.AppImage is Downloaded

Double Click, ProtonUp-Qt-2.6.5-x86_64.AppImage

Click, Integrate and Run

Proton-GE

Proton-GE Lutris Install Using .tar.gz

![](Images/image00697.jpeg)

Go to,

https://github.com/GloriousEggroll/proton-ge-custom/releases/tag/GE-Proton7-28

Click, GE-Proton7-28.tar.gz to Download GE-Proton7-28.tar.gz

Go to, Where GE-Proton7-28.tar.gz is Downloaded

Double Click, GE-Proton7-28.tar.gz

Double Click, GE-Proton7-28

Double Click, files

Select, All with Mouse Click and Drag or CTRL + A, while the window is focused

Click, Extract

Go to ~/.local/share/lutris/runners/wine

Click, Folder with +

Type In,

GE-Proton7-28

Click, Create

Extract to ~/.local/share/lutris/runners/wine/GE-Proton7-28

Proton-GE Steam Install Using .tar.gz

![](Images/image00698.jpeg)

Go to,

https://github.com/GloriousEggroll/proton-ge-custom/releases/tag/GE-Proton7-28

Click, GE-Proton7-28.tar.gz to Download GE-Proton7-28.tar.gz

Go to, Where GE-Proton7-28.tar.gz is Downloaded

Double Click, GE-Proton7-28.tar.gz

Select, All with Mouse Click and Drag or CTRL + A, while the application window is focused

Click, Extract

Go to ~/.steam/root

Click, Folder with +

Type In,

compatibilitytools.d

Click, Create

Go to ~/.steam/root/compatibilitytools.d

Click, Extract

WINE-GE

WINE-GE Lutris Install Using .tar.xz

![](Images/image00699.jpeg)

Go to,

[https://github.com/GloriousEggroll/wine-ge-custom/releases/tag/GE-Proton7-24](https://github.com/GloriousEggroll/wine-ge-custom/releases/tag/GE-Proton7-24)

Click,

wine-lutris-GE-Proton7-24-x86_64.tar.xz to Download

wine-lutris-GE-Proton7-24-x86_64.tar.xz

Go to, Where

wine-lutris-GE-Proton7-24-x86_64.tar.xz is Downloaded

Double Click,

wine-lutris-GE-Proton7-24-x86_64.tar.xz

Select, All with mouse click and drag or CTRL + A, while the application window is focused

DXVK

DXVK Install Using .sh Command Line

![](Images/image00700.jpeg)

Go to,

[https://github.com/doitsujin/dxvk/releases/tag/v1.10.3](https://github.com/doitsujin/dxvk/releases/tag/v1.10.3)

Click, dxvk-1.10.3.tar.gz to Download dxvk-1.10.3.tar.gz

Go to, Where dxvk-1.10.3.tar.gz is Downloaded

Double Click, dxvk.-1.10.3.tar.gz

Select, All

Extract, To ~/Downloads folder.

Go to, Where dxvk-1.10.3 is Extracted

Double Click, dxvk-1.10.3

Right Click, Empty Space

Click, Open in Terminal

Type In,

dir

Press, Enter

Type In,

./setup_dxvk.sh install --without-dxgi --with-d3d10 --symlink

Press, Enter

Default Prefix DXVK will install into is ~/.wine

VKD3D

VKD3D Install Using .sh Command Line

![](Images/image00701.jpeg)

Go to,

[https://github.com/HansKristian-Work/vkd3d-proton/releases/tag/v2.6](https://github.com/HansKristian-Work/vkd3d-proton/releases/tag/v2.6)

Click, vkd3d-proton-2.6.tar.zst to Download vkd3d-proton-2.6.tar.zst

Go to, Where vkd3d-proton-2.6.tar.zst is Downloaded

Double Click, vkd3d-proton-2.6.tar.zst

Extract, To ~/Downloads

Go to, Where vkd3d-proton-2.6 is Extracted

Double Click, vkd3d-proton-2.6

Right Click, Empty Space

Click, Open in Terminal

Type In,

dir

Type In,

./setup_vkd3d_proton.sh install --symlink

Press, Enter

Default Prefix VKD3D will install into is ~/.wine

Gnome Games

Gnome Games Install Using apt Command Line

![](Images/image00702.jpeg)

Open, Terminal

Type In,

sudo apt install gnome-games

Press, Enter

KDE Games

KDE Games Install Using apt Command Line

![](Images/image00703.jpeg)

Open, Terminal

Type In,

sudo apt install kdegames

Press, Enter

Music On Demand Streaming

Music On Demand Streaming services offer almost all music digitally available, with features like,

*   Creating your own playlist to keep private or share with those you wish
*   Exclusive streaming rights to certain artists music
*   Play the music you wish as you like

This chapter covers,

Amazon Music Unlimited

*   Amazon Music Unlimited Web Access

Apple Music

*   Apple Music Web Access

Spotify

*   Spotify Install Using Snap Store
*   Spotify Install Using snap Command Line
*   Spotify Web Access

Tidal

*   Tidal Web Access

Youtube Music

*   Youtube Music Web Access

Amazon Music Unlimited

Amazon Music Unlimited Web Access

![](Images/image00704.jpeg)

Go to,

[https://music.amazon.co.uk/](https://music.amazon.co.uk/)

Sign In, To access

Apple Music

Apple Music Web Access

![](Images/image00705.jpeg)

Go to,

[https://music.apple.com/us/browse](https://music.apple.com/us/browse)

Sign In, To access

Spotify

Spotify Install Using Snap Store

![](Images/image00706.jpeg)

Open, Snap Store

Type In,

spotify

Click, spotify

Click, Install

Spotify Install Using snap Command Line

![](Images/image00707.jpeg)

Open, Terminal

Type In,

sudo snap install spotify

Press, Enter

Spotify Web Access

![](Images/image00708.jpeg)

Go to,

[https://open.spotify.com/](https://open.spotify.com/)

Sign In, To access

Tidal

Tidal Web Access

![](Images/image00709.jpeg)

Go to,

[https://tidal.com/](https://tidal.com/)

Sign In, To access

Youtube Music

Youtube Music Web Access

![](Images/image00710.jpeg)

Go to,

[https://music.youtube.com/](https://music.youtube.com/)

Sign In, To access

Music Players

Music Players let users listen to their music and audio books, with additions such as,

*   Edit tags on audio files to better categorise music
*   Listening to internet radio stations
*   Search and play music uploaded to cloud services

This chapter covers,

Audacious

*   Audacious Install Using Software Manager
*   Audacious Install Using apt Command Line
*   Audacious Install Using flatpak Command Line

Clementine

*   Clementine Install Using Software Manager
*   Clementine Install Using apt Command Line
*   Clementine Install Using flatpak Command Line
*   Clementine Install Using Snap Store
*   Clementine Install Using snap Command Line

Deadbeef-vs

*   Deadbeef-vs Install Using Snap Store
*   Deadbeef-vs Install Using snap Command Line

Lollypop

*   Lollypop Install Using Software Manager
*   Lollypop Install Using apt Command Line
*   Lollypop Install Using flatpak Command Line

Rhythmbox

*   Rhythmbox Install Using Software Manager
*   Rhythmbox Install Using apt Command Line
*   Rhythmbox Install Using flatpak Command Line

Audacious

Audacious Install Using Software Manager

![](Images/image00711.jpeg)

Open, Software Manager

Type In,

audacious

Click, Audacious

Click, Install

Audacious Install Using apt Command Line

![](Images/image00712.jpeg)

Open, Terminal

Type In,

sudo apt install audacious

Press, Enter

Audacious Install Using flatpak Command Line

![](Images/image00713.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.atheme.audacious

Press, Enter

Clementine

Clementine Install Using Software Manager

![](Images/image00714.jpeg)

Open, Software Manager

Type In,

clementine

Click, Clementine

Click, Install

Clementine Install Using apt Command Line

![](Images/image00715.jpeg)

Open, Terminal

Type In,

sudo apt install clementine

Press, Enter

Clementine Install Using flatpak Command Line

![](Images/image00716.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.clementine_player.Clementine

Press, Enter

Clementine Install Using Snap Store

![](Images/image00717.jpeg)

Open, Snap Store

Type In,

clementine

Click, clementine

Click, Install

Clementine Install Using snap Command Line

![](Images/image00718.jpeg)

Open, Terminal

Type In,

sudo snap install clementine

Press, Enter

Deadbeef-vs

Deadbeef-vs Install Using Snap Store

![](Images/image00719.jpeg)

Open, Snap Store

Type In,

deadbeef

Click, deadbeef-vs

Click, Install

Deadbeef-vs Install Using snap Command Line

![](Images/image00720.jpeg)

Open, Terminal

Type In.

sudo snap install deadbeef-vs

Press, Enter

Lollypop

Lollypop Install Using Software Manager

![](Images/image00721.jpeg)

Open, Software Manager

Type In,

lollypop

Click, Lollypop

Click, Install

Lollypop Install Using apt Command Line

![](Images/image00722.jpeg)

Open, Terminal

Type In,

sudo apt install lollypop

Press, Enter

Lollypop Install Using flatpak Command Line

![](Images/image00723.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.gnome.Lollypop

Press, Enter

Rhythmbox

Rhythmbox Install Using Software Manager

![](Images/image00724.jpeg)

Open, Software Manager

Type In,

rhythmbox

Click, Rhythmbox

Click, Install

Rhythmbox Install Using apt Command Line

![](Images/image00725.jpeg)

Open, Terminal

Type In,

sudo apt install rhythmbox

Press, Enter

Rhythmbox Install Using flatpak Command Line

![](Images/image00726.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.gnome.Rhythmbox3

Press, Enter

Office Suites

Office Suites permit creating and editing documents, presentations, spreadsheets, in addition to,

*   Extensions that further existing, and create new, features
*   Compatible with various office document formats
*   Open source, paid for commercial and advert supported programs available

This chapter covers,

LibreOffice

*   LibreOffice Install Using Software Manager
*   LibreOffice Install Using apt Command Line
*   LibreOffice Install Using flatpak Command Line
*   LibreOffice Install Using Snap Store
*   LibreOffice Install Using snap Command Line

OnlyOffice

*   OnlyOffice Install Using Software Manager
*   OnlyOffice Install Using flatpak Command Line
*   OnlyOffice Install Using Snap Store
*   OnlyOffice Install Using snap Command Line
*   OnlyOffice Install Using .deb

OpenOffice

*   OpenOffice Install Using .AppImage

LibreOffice

LibreOffice Install Using Software Manager

![](Images/image00727.jpeg)

Open, Software Manager

Type In,

libreoffice

Click, LibreOffice

Click, Install

LibreOffice Install Using apt Command Line

![](Images/image00728.jpeg)

Open, Terminal

Type In,

sudo apt install libreoffice

Press, Enter

LibreOffice Install Using flatpak Command Line

![](Images/image00729.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.libreoffice.LibreOffice

Press, Enter

LibreOffice Install Using Snap Store

![](Images/image00730.jpeg)

Open, Snap Store

Type In,

libreoffice

Click, libreoffice

Click, Install

LibreOffice Install Using snap Command Line

![](Images/image00731.jpeg)

Open, Terminal

Type In,

sudo snap install libreoffice

Press, Enter

OnlyOffice

OnlyOffice Install Using Software Manager

![](Images/image00732.jpeg)

Open, Software Manager

Type In,

onlyoffice

Click, OnlyOffice Desktop Editors

Click, Install

OnlyOffice Install Using flatpak Command Line

![](Images/image00733.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.onlyoffice.desktopeditors

Press, Enter

OnlyOffice Install Using Snap Store

![](Images/image00734.jpeg)

Open, Snap Store

Type In,

onlyoffice

Click, onlyoffice-desktopeditors

Click, Install

OnlyOffice Install Using snap Command Line

![](Images/image00735.jpeg)

Open, Terminal

Type In,

sudo snap install onlyoffice-desktopeditors

Press, Enter

OnlyOffice Install Using .deb

![](Images/image00736.jpeg)

Go to,

[https://www.onlyoffice.com/en/download-desktop.aspx](https://www.onlyoffice.com/en/download-desktop.aspx)

Under, Debian 8, Ubuntu 14.04 and higher, Click, DOWNLOAD DEB to Download onlyoffice-desktopeditors_amd64.deb

Go to, Where onlyoffice-desktopeditors_amd64.deb is Downloaded

Double Click, onlyoffice-desktopeditors_amd64.deb

Click, Install

OpenOffice

OpenOffice Install Using .AppImage

![](Images/image00737.jpeg)

Go to,

[https://apprepo.de/appimage/openoffice](https://apprepo.de/appimage/openoffice)

Click, DOWNLOAD to Download OpenOffice.AppImage

Go to, Where OpenOffice.AppImage is Downloaded

Double Click, OpenOffice.AppImage

Click, Integrate and Run

Partition Managers

Partition Mangers let users easily control and manage disks, volumes and partitions, with features such as,

*   Create, Resize, Move and Check volumes and partitions
*   Support most, if not all, file systems
*   Have a go at rescuing data from damaged partitions

This chapter covers,

GParted

*   GParted Install Using Software Manager
*   GParted Install Using apt Command Line

KDE Partition Manager

*   KDE Partition Manager Install Using Software Manager
*   KDE Partition Manager Install Using apt Command Line

GParted

GParted Install Using Software Manager

![](Images/image00738.jpeg)

Open, Software Manager

Type In,

gparted

Click, GParted

Click, Install

GParted Install Using apt Command Line

![](Images/image00739.jpeg)

Open, Terminal

Type In,

sudo apt install gparted

Press, Enter

KDE Partition Manager

KDE Partition Manager Install Using Software Manager

![](Images/image00740.jpeg)

Open, Software Manager

Type In,

partition manager

Click, KDE Partition Manager

Click, Install

KDE Partition Manager Install Using apt Command Line

![](Images/image00741.jpeg)

Open, Terminal

Type In,

sudo apt install partitionmanager

Press, Enter

Password Managers

Password Managers let users securely create, edit and manage their passwords, with additions such as,

*   Securing passwords from any device or place
*   Password storage compliant with industry standards
*   Open source code that is vetted and improved upon by the global community

This chapter covers,

1Password

*   1Password Install Using .deb

Bitwarden

*   Bitwarden Install Using Software Manager
*   Bitwarden Install Using flatpak Command Line
*   Bitwarden Install Using Snap Store
*   Bitwarden Install Using snap Command Line
*   Bitwarden Install Using .deb

Buttercup

*   Buttercup Install Using .AppImage

KeePassXC

*   KeePassXC Install Using Software Manager
*   KeePassXC Install Using apt Command Line
*   KeePassXC Install Using flatpak Command Line
*   KeePassXC Install Using Snap Store
*   KeePassXC Install Using snap Command Line

LastPass

*   LastPass Universal Linux Installer Install Using .sh Command Line

1Password

1Password Install Using .deb

![](Images/image00742.jpeg)

Go to,

[https://1password.com/downloads/linux/](https://1password.com/downloads/linux/)

Click, Linux

Click, Download.deb to Download 1password-latest.deb

Go to, Where 1password-latest.deb is Downloaded

Double Click, 1password-latest.deb

Click, Install

Bitwarden

Bitwarden Install Using Software Manager

![](Images/image00743.jpeg)

Open, Software Manager

Type In,

bitwarden

Click, Bitwarden

Click, Install

Bitwarden Install Using flatpak Command Line

![](Images/image00744.jpeg)

Open, Terminal

Type In,

flatpak install flathub com.bitwarden.desktop

Press, Enter

Bitwarden Install Using Snap Store

![](Images/image00745.jpeg)

Open, Snap Store

Type In,

bitwarden

Click, bitwarden

Click, Install

Bitwarden Install Using snap Command Line

![](Images/image00746.jpeg)

Open, Terminal

Type In,

sudo snap install bitwarden

Press, Enter

Bitwarden Install Using .deb

![](Images/image00747.jpeg)

Go to,

https://github.com/bitwarden/desktop/releases

Click, Bitwarden-2022.5.1-amd64.deb to Download Bitwarden-2022.5.1-amd64.deb

Go to, Where Bitwarden-2022.5.1-amd64.deb is Downloaded

Double Click, Bitwarden-2022.5.1-amd64.deb

Click, Install

Buttercup

Buttercup Install Using .AppImage

![](Images/image00748.jpeg)

Go to,

[https://github.com/buttercup/buttercup-desktop/releases/tag/v2.16.0](https://github.com/buttercup/buttercup-desktop/releases/tag/v2.16.0)

Click, Buttercup-linux-x86_64.AppImage to Download Buttercup-linux-x86_64.AppImage

Go to, Where Buttercup-linux-x86_64.AppImage is Downloaded

Double Click, Buttercup-linux-x86_64.AppImage

Click, Integrate and Run

KeePassXC

KeePassXC Install Using Software Manager

![](Images/image00749.jpeg)

Open, Software Manager

Type In,

keepassxc

Click, KeePassXC

Click, Install

KeePassXC Install Using apt Command Line

![](Images/image00750.jpeg)

Open, Terminal

Type In,

sudo apt install keepassxc

Press, Enter

KeePassXC Install Using flatpak Command Line

![](Images/image00751.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.keepassxc.KeePassXC

Press, Enter

KeePassXC Install Using Snap Store

![](Images/image00752.jpeg)

Open, Snap Store

Type In,

keepassxc

Click, keepassxc

Click, Install

KeePassXC Install Using snap Command Line

![](Images/image00753.jpeg)

Open, Terminal

Type In,

sudo snap install keepassxc

Press, Enter

LastPass

LastPass Universal Linux Installer Install Using .sh Command Line

![](Images/image00754.jpeg)

Go to,

https://lastpass.com/lplinux.php

Click, lplinux.tar.bz2 to Download lplinux.tar.bz2

Go to, Where lplinux.tar.bz2 is Downloaded

Double Click, lplinux.tar.bz2

Select, All with mouse click and drag or press CTRL + A

Extract, To ~/Downloads/lplinux

(Create folder with folder+ and create, if folder does not already exist)

Go to, ~/Downloads/lplinux

Right Click, Empty Space

Click, Open in Terminal

Type In,

dir

Press, Enter

Type In,

./install_lastpass.sh

Press, Enter

Remote Working

Remote Working software permits users to work on products and collaborate with colleagues, and issued with features such as,

*   Giving ideas to work colleagues and viewing the project improve in real time
*   Shared cloud or local document storage
*   Online meetings with potentially all employees present

This chapter covers,

Citrix

*   Citrix Install Using .deb

Microsoft Teams

*   Microsoft Teams Install Using Snap Store
*   Microsoft Teams Install Using snap Command Line

Slack

*   Slack Install Using .deb

Zoom

*   Zoom Install Using .deb

Citrix

Citrix Install Using .deb

![](Images/image00755.jpeg)

Go to,

[https://www.citrix.com/downloads/workspace-app/linux/workspace-app-for-linux-latest.html](https://www.citrix.com/downloads/workspace-app/linux/workspace-app-for-linux-latest.html)

Click, Debian Packages

Click, Full Packages

Under, Citrix Workspace app for Linux (x86_64)

Click, Download File to Download icaclient_22.7.0.20_amd64.deb

Go to, Where icaclient_22.7.0.20_amd64.deb is Downloaded

Double Click, icaclient_22.7.0.20_amd64.deb

Click, Install

Microsoft Teams

Microsoft Teams Install Using Snap Store

![](Images/image00756.jpeg)

Open, Snap Store

Type In,

microsoft teams

Click, Microsoft Teams - Insiders

Click, Install

Microsoft Teams Install Using snap Command Line

![](Images/image00757.jpeg)

Open, Terminal

Type In,

sudo snap install teams

Press, Enter

Slack

Slack Install Using .deb

![](Images/image00758.jpeg)

Go to,

https://slack.com/intl/en-gb/downloads/linux

Click, Download .DEB app to Download slack-desktop-4.27.156-amd64.deb

Go to, Where slack-desktop-4.27.156-amd64.deb is Downloaded

Double Click, slack-desktop-4.27.156-amd64.deb

Click, Install

Zoom

Zoom Install Using .deb

![](Images/image00759.jpeg)

Go to,

https://zoom.us/download?os=linux

Click, Box in the same row as Linux Type

Click, Ubuntu

Click, Box In the same row as OS Architecture

Click, 64 bit

Click, Box in the same row as Version

Click, 16.04+

Click, Download to Download zoom_amd64.deb

Go to, Where zoom_amd64.deb is Downloaded

Double Click, zoom_amd64.deb

Click, Install

Sandbox

Sandboxing helps to keep Linux Mint 21 secure by, seperating certain programs from others, and includes,

*   Seperated programs have their own individual view of system resources
*   Capable of sandboxing any piece of  software or system process
*   Accesible two click graphical interface

This chapter covers,

Firejail

*   Firejail Install Using Software Manager
*   Firejail Install Using apt Command Line

Firetools

*   Firetools Install Using Software Manager
*   Firetools Install Using apt Command Line

Firejail

Firejail Install Using Software Manager

![](Images/image00760.jpeg)

Open, Software Manager

Type In,

firejail

Click, Firejail

Click, Install

Firejail Install Using apt Command Line

![](Images/image00761.jpeg)

Open, Terminal

Type In,

sudo apt install firejail

Press, Enter

Firetools

Firetools Install Using Software Manager

![](Images/image00762.jpeg)

Open, Software Manager

Type In,

firetools

Click, Firetools

Click, Install

Firetools Install Using apt Command Line

![](Images/image00763.jpeg)

Open, Terminal

Type In,

sudo apt install firetools

Press, Enter

Software Distribution

Software Distribution is about increasing the number of ways that software can be installed, in Linux Mint 21, with platform features such as,

*   Automatic and/or manual updating of programs
*   Selection of format or source to use
*   Showing dependecies that are required for installation

This chapter covers,

AppImageLauncher

*   AppImageLauncher Install Using apt Command Line
*   AppImage Launcher Install Using .deb

Flatpak

*   Flatpak Install Using apt Command Line

Flathub

*   Flathub Repo Add Using flatpak Command Line

Snap

*   Snap Install Using apt Command Line

Snap Store

*   Snap Store Install Using snap Command Line

Java

*   Java Install Using .deb

Ocs-url

*   Ocs-url Install Using .deb

Open Java

*   Open Java JRE and JDK Install Using apt Command Line

deb-get

*   deb-get Install using curl Command Line

App Outlet

*   App Outlet Install Using .deb

pacstall

*   pacstall Install Using curl Command Line

AppImageLauncher

AppImageLauncher Install Using apt Command Line

![](Images/image00764.jpeg)

Open, Terminal

Type In,

sudo add-apt-repository ppa:appimagelauncher-team/stable && sudo apt update && sudo apt install appimagelauncher

Press, Enter

AppImage Launcher Install Using .deb

![](Images/image00765.jpeg)

Go to,

[https://github.com/TheAssassin/AppImageLauncher/releases/tag/v2.2.0](https://github.com/TheAssassin/AppImageLauncher/releases/tag/v2.2.0)

Click, appimagelauncher_2.2.0-travis995-0f91801.bionic_amd64.deb to Download appimagelauncher_2.2.0-travis995-0f91801.bionic_amd64.deb

Go to, Where appimagelauncher_2.2.0-travis005-0f91801.bionic_amd64.deb is Downloaded

Double Click, appimagelauncher_2.2.0-travis005-0f91801.bionic_amd64.deb

Click, Install

Flatpak

Flatpak Install Using apt Command Line

![](Images/image00766.jpeg)

Open, Terminal

Type In,

sudo apt install flatpak

Press, Enter

Flathub

Flathub Repo Add Using flatpak Command Line

![](Images/image00767.jpeg)

Open, Terminal

Type In,

flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

Press, Enter

Afterwards, Restart PC

Snap

Snap Install Using apt Command Line

![](Images/image00768.jpeg)

Open, Terminal

Type In,

sudo mv /etc/apt/preferences.d/nosnap.pref ~/Documents/nosnap.backup

Press, Enter

![](Images/image00769.jpeg)

Type In,

sudo apt update && sudo apt install snapd

Press, Enter

Afterwards, Restart PC

Snap Store

Snap Store Install Using snap Command Line

![](Images/image00770.jpeg)

Open, Terminal

Type In,

sudo snap install snap-store

Press, Enter

Afterwards, Restart PC

Java

Java Install Using .deb

![](Images/image00771.jpeg)

Go to,

[https://www.oracle.com/java/technologies/downloads/](https://www.oracle.com/java/technologies/downloads/)

Click, Linux

In, The same row as x64 Debian Package, Click, the link in the Download column, To Download jdk-18_linux-x64_bin.deb

Go to, Where jdk-18_linux-x64_bin.deb is Downloaded

Double Click, jdk-18_linux-x64_bin.deb

Click, Install

Ocs-url

Ocs-url Install Using .deb

![](Images/image00772.jpeg)

Go to,

[https://www.opendesktop.org/p/1136805/](https://www.opendesktop.org/p/1136805/)

Click, Download

Click, ocs-url_3.1.0-0ubuntu1_amd64deb

Click, Download to Download ocs-url_3.1.0-0ubuntu1_amd64.deb

Go to, Where ocs-url_3.1.0-0ubuntu1_amd64.deb is Downloaded

Double Click, ocs-url_3.1.0-0ubuntu1_amd64.deb

Click, Install

Open Java

Open Java JRE and JDK Install Using apt Command Line

![](Images/image00773.jpeg)

Open, Terminal

Type In,

sudo apt install default-jre default-jdk

Press, Enter

deb-get

deb-get Install using curl Command Line

![](Images/image00774.jpeg)

Open, Terminal

Type In,

sudo apt install curl

Press, Enter

![](Images/image00775.jpeg)

Open, Terminal

Type In,

curl -sL https://raw.githubusercontent.com/wimpysworld/deb-get/main/deb-get | sudo -E bash -s install deb-get

Press, Enter

App Outlet

App Outlet Install Using .deb

![](Images/image00776.jpeg)

Go to,

[https://github.com/app-outlet/app-outlet/releases/tag/v2.1.0](https://github.com/app-outlet/app-outlet/releases/tag/v2.1.0)

Click, app-outlet_2.1.0_amd64.deb to Download, app-outlet-2.1.0_amd64.deb

Go to, Where app-outlet_2.1.0_amd64.deb is Downloaded

Double Click, app-outlet_2.1.0_amd64.deb

Click, Install

pacstall

pacstall Install Using curl Command Line

![](Images/image00777.jpeg)

Open, Terminal

Type In,

sudo bash -c "$(curl -fsSL https://git.io/JsADh || wget -q https://git.io/JsADh -O -)"

Press, Enter

Streaming

Streaming software transmits AV to a remote server with additions like,

*   Adding objects and items to the video feed through scenes and elements
*   Changing quality to best suit the internet connection
*   Stream and record at the same time to keep local copies of broadcasts

This chapter covers,

OBS Studio

*   OBS Studio Install Using Software Manager
*   OBS Studio Install Using apt Command Line
*   OBS Studio Install Using flatpak Command Line
*   OBS Studio Install Using Snap Store
*   OBS Studio Install Using snap Command Line
*   OBS Studio Install deb-get Command Line

Owncast

*   Owncast Install Using curl Command Line

OBS Studio

OBS Studio Install Using Software Manager

![](Images/image00778.jpeg)

Open, Software Manager

Type In,

obs studio

Click, OBS Studio

Click, Install

OBS Studio Install Using apt Command Line

![](Images/image00779.jpeg)

Open, Terminal

Type In,

sudo apt install obs-studio

Press, Enter

OBS Studio Install Using flatpak Command Line

![](Images/image00780.jpeg)

Open, Terminal

Type In,

flatpak install flathub com.obsproject.Studio

Press, Enter

OBS Studio Install Using Snap Store

![](Images/image00781.jpeg)

Open, Snap Store

Type In,

obs studio

Click, OBS Studio

Click, Install

OBS Studio Install Using snap Command Line

![](Images/image00782.jpeg)

Open, Terminal

Type In,

sudo snap install obs-studio

Press, Enter

OBS Studio Install deb-get Command Line

![](Images/image00783.jpeg)

Open, Terminal

Type In,

sudo deb-get install obs-studio

Press, Enter

Owncast

Owncast Install Using curl Command Line

![](Images/image00784.jpeg)

Open, Terminal

Type In,

curl -s https://owncast.online/install.sh | bash

Press, Enter

System Cleaners

System Cleaners help to remove junk and excess files from the system, to increase space, but can also,

*   Add, Remove or Disable startup applications
*   Manage the hosts file to allow and block websites
*   View a dashboard that displays important visualized data at a glance

This chapter covers,

Bleachbit

*   Bleachbit Install Using Software Manager
*   Bleahbit Install Using apt Command Line

Czkawka

*   Czkawka Install Using Software Manager
*   Czkawka Install Using flatpak Command Line
*   Czkawka Install Using Snap Store
*   Czkawka Install Using snap Command Line

FSlint Unofficial

*   FSlint Unofficial Install Using Snap Store
*   FSlint Unofficial Install Using snap Command Line

Stacer

*   Stacer Install Using Software Manager
*   Stacer Install Using apt Command Line

Synaptic Package Manager

*   Synpatic Package Manager Install Using Software Manager
*   Synaptic Package Manager Install Using apt Command Line

Sweeper

*   Sweeper Install Using Software Manager
*   Sweeper Install Using apt Command Line

Bleachbit

Bleachbit Install Using Software Manager

![](Images/image00785.jpeg)

Open, Software Manager

Type In,

bleachbit

Click, Bleachbit

Click, Install

Bleachhbit Install Using apt Command Line

![](Images/image00786.jpeg)

Open, Terminal

Type In,

sudo apt install bleachbit

Press, Enter

Czkawka

Czkawka Install Using Software Manager

![](Images/image00787.jpeg)

Open, Software Manager

Type In,

czkawka

Click, Czkawka

Click, Install

Czkawka Install Using flatpak Command Line

![](Images/image00788.jpeg)

Open, Terminal

Type In,

flatpak install flathub com.github.qarmin.czkawka

Press, Enter

Czkawka Install Using Snap Store

![](Images/image00789.jpeg)

Open, Snap Store

Type In,

czkawka

Click, czkawka

Click, Install

Czkawka Install Using snap Command Line

![](Images/image00790.jpeg)

Open, Terminal

Type In,

sudo snap install czkawka

Press, Enter

FSlint Unofficial

FSlint Unofficial Install Using Snap Store

![](Images/image00791.jpeg)

Open, Snap Store

Type In,

fslint

Click, fslint-unofficial

Click, Install

FSlint Unofficial Install Using snap Command Line

![](Images/image00792.jpeg)

Open, Terminal

Type In,

sudo snap install fslint-unofficial

Press, Enter

Stacer

Stacer Install Using Software Manager

![](Images/image00793.jpeg)

Open, Software Manager

Type In,

stacer

Click, Stacer

Click, Install

Stacer Install Using apt Command Line

![](Images/image00794.jpeg)

Open, Terminal

Type In,

sudo apt install stacer

Press, Enter

Synaptic Package Manager

Synpatic Package Manager Install Using Software Manager

![](Images/image00795.jpeg)

Open, Software Manager

Type In,

synaptic

Click, Synaptic Package Manager

Click, Install

Synaptic Package Manager Install Using apt Command Line

![](Images/image00796.jpeg)

Open, Terminal

Type In,

sudo apt install synaptic

Press, Enter

Sweeper

Sweeper Install Using Software Manager

![](Images/image00797.jpeg)

Open, Software Manager

Type In,

sweeper

Click, Sweeper

Click, Install

Sweeper Install Using apt Command Line

![](Images/image00798.jpeg)

Open, Terminal

Type In,

sudo apt install sweeper

Press, Enter

System Settings

System Settings are concerned with keeping the system and it’s packages up to date, with the ability for the user to configure the system, to beings liking, and can include,

*   Keeping Graphics and Other Additional Drivers Up to Date
*   Updating Linux Mint 21 and Other Packages
*   Adding more up to date versions of drivers through PPA’s

This chapter covers,

32 Bit Architecture

*   32 Bit Architecture Install Using apt Command Line

Alternative DNS Servers

*   Alternative DNS Services Setup Using Network
*   List of Other Alternate DNS Services

Auto Mount Disks

*   Auto Mount Disks Using Disks

Graphics Drivers

*   AMD Graphics Drivers Install Using apt Command Line
*   AMD Graphics Driver Default Using ppa-purge Command Line
*   Nvidia Graphics Driver Install Using Software Manager
*   Nvidia Graphics Driver Install Using apt Command Line

Mousepad

*   Mousepad Install Using Software Manager
*   Mousepad Install Using apt Command Line

Mouse Speed

*   Setting Mouse Speed to Max

Night Light

*   Setting Up Night Light (Blue Light Protection)

Possible Intel Sound Crackle Fix

*   Possible Intel Sound Crackle Fix Using echo Command Line

Purge PPA’s

*   Purge PPA’s Using Software Sources
*   PPA Purge Install
*   Purge PPA’s Using ppa-purge Command Line

Set Default Application

*   Set Default Application for Category
*   Set Default Application Per File Extension

Startup Applications

*   Startup Applications Using Installed Applications
*   Startup Applications Using Custom Commands

Uninstalling Applications

*   Uninstall Software Manager Applications
*   Uninstall apt Command Line Applications
*   Uninstall Snap Store Installed Applications
*   Uninstall snap Command Line Applications
*   Uninstalling deb-get Command Line Applications

Updating Linux Mint 21

*   Updating Linux Mint 21 Using Update Manager
*   Updating Linux Mint 21 Using apt Command Line

Updating Linux Mint 21 Kernel

*   Updating Linux Mint 21 Kernel Using Update Manager

32 Bit Architecture

32 Bit Architecture Install Using apt Command Line

![](Images/image00799.jpeg)

Open, Terminal

Type In,

sudo dpkg --add-architecture i386

Press, Enter

Alternative DNS Servers

Alternative DNS Services Setup Using Network

![](Images/image00800.jpeg)

Open, Network

Click, Cog Icon in the same row as Connected Connection that can access the internet

![](Images/image00801.jpeg)

Click, IPv4

Move, Switch in the same row as  DNS and Automatic to the left

Click, + under DNS

Click, 1st Box in the same row as Server

Type In,

84.200.69.80

Click, 2nd Box In the same row as Server

Type In,

84.200.70.40

Click, IPv6

![](Images/image00802.jpeg)

Move, Switch in the same row as DNS and Automatic to the left

Click, + under DNS

Click, 1st Box in the same row as Server

Type In,

2001:1608:10:25::1c04:b12f

Click, 2nd Box In the same row as Server

Type In,

2001:1608:10:25::9249:d69b

Click, Apply

Move Switch, In the same row as Network connected to the internet, To the Left and Right (with a reasonable gap in between) to propagate changes

List of Other Alternate DNS Services

CleanBrowsing

[https://cleanbrowsing.org/filters/](https://cleanbrowsing.org/filters/)

IPv4,

185.228.168.168

185.228.169.168

IPv6,

2a0d:2a00:1::

2a0d:2a00:2::

DNS-Over HTTPS (DOH),

https://doh.cleanbrowsing.org/doh/family-filter/

DNS-Over-TLS (DOT),

family-filter-dns.cleanbrowsing.org

FOURTHESTATE

https://www.fourthestate.org/

IPv4,

45.77.165.194

45.32.36.36

DNS.WATCH

https://dns.watch/

IPv4,

84.200.69.80

84.200.70.40

IPv6,

2001:1608:10:25::1c04:b12f

2001:1608:10:25::9249:d69b

DNS-Over HTTPS (DOH),

https://resolver2.dns.watch/dns-query

quad9

[https://www.quad9.net/service/service-addresses-and-features/](https://www.quad9.net/service/service-addresses-and-features/)

IPv4,

9.9.9.9

149.112.112.112

IPv6

2620:fe::fe

2620:fe::9

DNS-Over HTTPS (DOH),

https://dns.quad9.net/dns-query

DNS-Over-TLS (DOT),

tls://dns.quad9.net

Auto Mount Disks

Auto Mount Disks Using Disks

![](Images/image00803.jpeg)

Open, Disks

Select, Disk

Select, Volume

Click, Cog or Additional partition options icon

Click, Edit Mount Options

Move, Button in the same row as, User Session Defaults, to the left

Click, OK

Graphics Drivers

AMD Graphics Drivers Install Using apt Command Line

AMD Graphics Drivers are pre-installed with Linux Mint 21 and the Linux Kernel, in addition to being tested to reasonable satisfaction by the Linux Mint Team , The Linux Mint Community and the Linux Mark Institute.

However these AMD Drivers, while being the most stable, are not the most up to date, and the ones below are the most up to date, but not, neccesarily, the most stable.

![](Images/image00804.jpeg)

Open, Terminal

Type In,

sudo add-apt-repository ppa:oibaf/graphics-drivers

Press, Enter

![](Images/image00805.jpeg)

Type In,

sudo apt update && sudo apt upgrade

Press, Enter

AMD Graphics Driver Default Using ppa-purge Command Line

![](Images/image00806.jpeg)

Open, Terminal

Type In,

sudo apt install ppa-purge

Press, Enter

![](Images/image00807.jpeg)

Type In,

sudo ppa-purge ppa:oibaf/graphics-drivers && sudo apt update && sudo apt upgrade

Press, Enter

Nvidia Graphics Driver Install Using Software Manager

![](Images/image00808.jpeg)

Open, Driver Manager

Click, Circle in the same row as Nvidia-515

Click, Apply Changes

Nvidia Graphics Driver Install Using apt Command Line

![](Images/image00809.jpeg)

Open, Terminal

Type In

sudo apt install nvidia-driver-515

Press, Enter

Mousepad

Mousepad Install Using Software Manager

![](Images/image00810.jpeg)

Open, Software Manager

Type In,

mousepad

Click, Mousepad

Click, Install

Mousepad Install Using apt Command Line

![](Images/image00811.jpeg)

Open, Terminal

Type In,

sudo apt install mousepad

Press, Enter

Mouse Speed

Setting Mouse Speed to Max

![](Images/image00812.jpeg)

Open, Mouse and Touchpad

Move, Switch in the same row as Custom Acceleration to the Right

Move, Button under Speed to the Right

Night Light

Setting Up Night Light (Blue Light Protection)

Open, Redshift

Right Click, Redshift Icon on the taskbar

Tick, Box in the same row as Autostart

Possible Intel Sound Crackle Fix

Possible Intel Sound Crackle Fix Using echo Command Line

![](Images/image00813.jpeg)

Open, Terminal

Type In,

echo "options snd_hda_intel power_save=0" | sudo tee -a /etc/modprobe.d/audio_disable_powersave.conf

Press, Enter

Purge PPA’s

Purge PPA’s Using Software Sources

![](Images/image00814.jpeg)

Open, Software Sources

Click, PPA’s

Select, Oibaf

Click, Remove

Click, OK

PPA Purge Install

![](Images/image00806.jpeg)

Open, Terminal

Type In,

sudo apt install ppa-purge

Press, Enter

Purge PPA’s Using ppa-purge Command Line

![](Images/image00807.jpeg)

Open, Terminal

Type In,

sudo ppa-purge ppa:oibaf/graphics-drivers && sudo apt update && sudo apt upgrade

Set Default Application

Set Default Application for Category

![](Images/image00815.jpeg)

Open, Preferred Applications

Click, Box In the same row as Video

Click, VLC

Set Default Application Per File Extension

![](Images/image00816.jpeg)

Right Click, Winter Veil Christmas Music - World of Warcraft Music.webm

Click, Properties

Click, Open With

Select, VLC

Click, Set as Default

Startup Applications

Startup Applications Using Installed Applications

![](Images/image00817.jpeg)

Open, Startup Applications

Click, +

Click, Choose application

Type In, discord

Select, Discord

Click, Add Application

Startup Applications Using Custom Commands

![](Images/image00818.jpeg)

Open, Startup Applications

Click, +

Click, Custom command

Click, Box in the same row as Name

Type In,

Discord

Click, Box in in the same row as Command

Type In,

discord

Click, Add

Uninstalling Applications

Uninstall Software Manager Applications

![](Images/image00819.jpeg)

Open, Software Manager

Type In,

gimp

Select, Gimp or Gnu Image Manipulation Program

Click, Remove

Uninstall apt Command Line Applications

![](Images/image00820.jpeg)

Open, Terminal

Type In,

sudo apt remove parole

Press, Enter

Uninstall Snap Store Installed Applications

![](Images/image00821.jpeg)

Open, Snap Store

Click, Installed

Click, Uninstall in the same row as litteris

Uninstall snap Command Line Applications

![](Images/image00822.jpeg)

Open, Terminal

Type In,

sudo snap remove coin

Press, Enter

Uninstalling deb-get Command Line Applications

![](Images/image00823.jpeg)

Open, Terminal

Type In,

sudo deb-get remove obs-studio

Press, Enter

Updating Linux Mint 21

Updating Linux Mint 21 Using Update Manager

![](Images/image00824.jpeg)

Open, Update Manager

Select, Updates to Install

Click, Install Updates

Updating Linux Mint 21 Using apt Command Line

![](Images/image00805.jpeg)

Open, Terminal

Type In,

sudo apt update && sudo apt upgrade

Press, Enter

Updating Linux Mint 21 Kernel Using Update Manager

![](Images/image00825.jpeg)

Open, Update Manager

Click, View

Click, Linux Kernels

Select, Kernel Of Choice

Click, Install

System Utilities

System Utilities permit the monitoring of the systems status and shows actions that could be taken, such as,

*   S.M.A.R.T (Self-Monitoring, Analysis and Reporting Technology)
*   Estimated remaining life time of internal parts
*   Showing details system components and software information

This chapter covers,

Cpufetch

*   Cpufetch Install Using apt Command Line

CPU-X

*   CPU-X Install Using .AppImage

Gpustat

*   Gpustat Install Using apt Command Line

Hard Disk Sentinel

*   Hard Disk Sentinel Install Using .tar.xz

Neofetch

*   Neofetch Install Using apt Command Line

System Profiler and Benchmark

*   System Profiler and Benchmark Install Using Software Manager
*   System Profiler and Benchmark Install Using apt Command Line

Psensor

*   Psensor Install Using apt Command Line

Cpufetch

Cpufetch Install Using apt Command Line

![](Images/image00826.jpeg)

Open, Terminal

Type In,

sudo apt install cpufetch

Press, Enter

To Run, Cpufetch,

Type In,

cpufetch

Press, Enter

CPU-X

CPU-X Install Using .AppImage

![](Images/image00827.jpeg)

Go to,

[https://github.com/X0rg/CPU-X/releases/tag/v4.3.1](https://github.com/X0rg/CPU-X/releases/tag/v4.3.1)

Click, CPU-X-v4.3.1-x86_64.AppImage to Download CPU-X-v4.3.1-x86_64.AppImage

Go to, Where CPU-X-v4.3.1-x86_64.AppImage is Downloaded

Double Click, CPU-X-v4.3.1-x86_64.AppImage

Click, Integrate and Run

Gpustat

Gpustat Install Using apt Command Line

![](Images/image00828.jpeg)

Open, Terminal

Type In,

sudo apt install gpustat

Press, Enter

To Run, Type In,

gpustat

Press, Enter

Hard Disk Sentinel

Hard Disk Sentinel Install Using .tar.xz

![](Images/image00829.jpeg)

Go to,

[https://www.hdsentinel.com/hard_disk_sentinel_linux_gui.php](https://www.hdsentinel.com/hard_disk_sentinel_linux_gui.php)

Click, hdsentinel_gui64bit.tar.xz to Download hdsentinel_gui64bit.tar.xz

Go to, Where hdsentinel_gui64bit.tar.xz is Downloaded

Double Click, hdsentinel_gui64bit.tar.xz

Double Click, HDSentinel_GUI

Double Click, HDSentinel_GUI.zip

Select, HDSentinel_GUI

Extract, To ~/Applications

To Run, Go to, Where HDSentinel_GUI was extracted

Double Click, HDSentinel_GUI

Double Click, HDSentinel_GUI

Neofetch

Neofetch Install Using apt Command Line

![](Images/image00830.jpeg)

Open, Terminal

Type In,

sudo apt install neofetch

Press, Enter

System Profiler and Benchmark

System Profiler and Benchmark Install Using Software Manager

![](Images/image00831.jpeg)

Open, Software Manager

Type In,

hardinfo

Click, System Profiler and Benchmark

Click, Install

System Profiler and Benchmark Install Using apt Command Line

![](Images/image00832.jpeg)

Open, Terminal

Type In,

sudo apt install hardinfo

Press, Enter

Psensor

Psensor Install Using apt Command Line

![](Images/image00833.jpeg)

Open, Terminal

Type In,

sudo apt install lm-sensors

Press, Enter

![](Images/image00834.jpeg)

Type In,

sudo sensors-detect

Press, Enter

![](Images/image00835.jpeg)

Type In,

sensors

Press, Enter

![](Images/image00836.jpeg)

Type In,

sudo apt install psensor

Press, Enter

Video Editors

Video Editors are software permitting the editing and generation of video, with audio and include features such as,

*   Import and export different video file formats
*   Converting between different file formats and video quality
*   Recording video from inputs, and storing them directly

This chapter covers,

Flowblade

*   Flowblade Install Using Software Manager
*   Flowblade Install Using apt Command Line
*   Flowblade Install Using flatpak Command Line

Kdenlive

*   Kdenlive Install Using Software Manager
*   Kdenlive Install Using apt Command Line
*   Kdenlive Install Using flatpak Command Line
*   Kdenlive Install Snap Store
*   Kdenlive Install Using snap Command Line

Openshot

*   Openshot Install Using Software Manager
*   Openshot Install Using apt Command Line
*   Openshot Install Using flatpak Command Line
*   Openshot Install Using .AppImage

Shotcut

*   Shotcut Install Using Software Manager
*   Shotcut Install Using apt Command Line
*   Shotcut Install Using flatpak Command Line
*   Shotcut Install Using Snap Store
*   Shotcut Install Using snap Command Line

Flowblade

Flowblade Install Using Software Manager

![](Images/image00837.jpeg)

Open, Software Manager

Type In,

flowblade

Click, Flowblade

Click, Install

Flowblade Install Using apt Command Line

![](Images/image00838.jpeg)

Open, Terminal

Type In,

sudo apt install flowblade

Press, Enter

Flowblade Install Using flatpak Command Line

![](Images/image00839.jpeg)

Open, Terminal

Type In,

flatpak install flathub io.github.jliljebl.Flowblade

Press, Enter

Kdenlive

Kdenlive Install Using Software Manager

![](Images/image00840.jpeg)

Open, Software Manager

Type In,

kdenlive

Click, Kdenlive

Click, Install

Kdenlive Install Using apt Command Line

![](Images/image00841.jpeg)

Open, Terminal

Type In,

sudo apt install kdenlive

Press, Enter

Kdenlive Install Using flatpak Command Line

![](Images/image00842.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.kde.kdenlive

Press, Enter

Kdenlive Install Snap Store

![](Images/image00843.jpeg)

Open, Snap Store

Type In,

kdenlive

Click, kdenlive

Click, Install

Kdenlive Install Using snap Command Line

![](Images/image00844.jpeg)

Open, Terminal

Type In,

sudo snap install kdenlive

Press, Enter

Openshot

Openshot Install Using Software Manager

![](Images/image00845.jpeg)

Open, Software Manager

Type In,

openshot

Click, Openshot

Click, Install

Openshot Install Using apt Command Line

![](Images/image00846.jpeg)

Open, Terminal

Type In,

sudo apt install openshot

Press, Enter

Openshot Install Using flatpak Command Line

![](Images/image00847.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.openshot.OpenShot

Press, Enter

Openshot Install Using .AppImage

![](Images/image00848.jpeg)

Go to,

[https://www.openshot.org/download/](https://www.openshot.org/download/)

Click, Download v2.6.1 to Download OpenShot-v2.6.1-x86_64.AppImage

Go to, Where OpenShot-v2.6.1 is Downloaded

Double Click, OpenShot-v2.6.1

Click, Integrate and Run

Shotcut

Shotcut Install Using Software Manager

![](Images/image00849.jpeg)

Open, Software Manager

Type In,

shotcut

Click, Shotcut

Click, Install

Shotcut Install Using apt Command Line

![](Images/image00850.jpeg)

Open, Terminal

Type In,

sudo apt install shotcut

Press, Enter

Shotcut Install Using flatpak Command Line

![](Images/image00851.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.shotcut.Shotcut

Press, Enter

Shotcut Install Using Snap Store

![](Images/image00852.jpeg)

Open, Snap Store

Type In,

shotcut

Click, shotcut

Click, Install

Shotcut Install Using snap Command Line

![](Images/image00853.jpeg)

Open, Terminal

Type In,

sudo snap install shotcut

Press, Enter

Video On Demand Streaming

Video On Demand Streaming services offer most tv series and movies digitally available, with features like,

*   Profiles to keep different watchers habits, seperated
*   Exclusive streaming rights to certain TV shows and movies
*   Watch for as long as the media is available

This chapter covers,

Amazon Prime Video

*   Amazon Prime Video Access

Disney+

*   Disney+ Access

Netflix

*   Netflix Access

Paramount+

*   Paramount+ Access

Amazon Prime Video

Amazon Prime Video Access

![](Images/image00854.jpeg)

Go to,

[https://www.amazon.co.uk/Amazon-Video/b?node=3010085031](https://www.amazon.co.uk/Amazon-Video/b?node=3010085031)

Sign In, To Access Amazon Prime Video

Disney+

Disney+ Access

![](Images/image00855.jpeg)

Go to,

[https://www.disneyplus.com/en-gb](https://www.disneyplus.com/en-gb)

Sign In, To Access Disney+

Netflix

Netflix Access

![](Images/image00856.jpeg)

Go to,

[https://www.netflix.com/gb/](https://www.netflix.com/gb/)

Sign In, To Access Netflix

Paramount+

Paramount+ Access

![](Images/image00857.jpeg)

Go to,

[https://www.paramountplus.com/gb/](https://www.paramountplus.com/gb/)

Sign In, To Access Paramount+

Virtualization

Virtualization permits running of other operating systems, to run games or software and include,

*   Changing the host resources available to each Virtual Machine
*   Permitting varying access between the host and client VM
*   Extension packs that increase and empower features

This chapter covers,

Virt-manager

*   Virt-manager Install Using apt Command Line

Virtualbox

*   Virtualbox Install Using Software Manager
*   Virtualbox Install Using apt Command Line

Virt-manager

Virt-manager Install Using apt Command Line

![](Images/image00858.jpeg)

Open, Terminal

Type In,

sudo apt install qemu-kvm libvirt-clients libvirt-daemon-system bridge-utils virtinst libvirt-daemon && virt-manager

Press, Enter

![](Images/image00859.jpeg)

Type In,

sudo systemctl enable --now libvirtd

Press, Enter

Virtualbox

Virtualbox Install Using Software Manager

![](Images/image00860.jpeg)

Open, Software Manager

Type In,

virtualbox

Click, Virtualbox

Click, Install

Virtualbox Install Using apt Command Line

![](Images/image00861.jpeg)

Open, Terminal

Type In,

sudo apt install virtualbox && sudo apt install virtualbox-guest-additions-iso && sudo apt install virtualbox-ext-pack

Press, Enter

Web Browsers

Web Browsers let the user surf or browse the internet, and come with various features such as,

*   Extensions that add to or increase features
*   Built in download managers that let users easily manage files
*   Account syncing that transfers extensions and settings across multiple devices

This chapter covers,

Firefox

Firefox Install Using Software Manager

*   Firefox Install Using apt Command Line
*   Firefox Install Using flatpak Command Line
*   Firefox Install Using Snap Store
*   Firefox Install Using snap Command Line

Firefox ESR

*   Firefox ESR Install Using .tar.gz

Chromium

*   Chromium Install Using Snap Store
*   Chromium Install Using snap Command Line

Google Chrome

*   Google Chrome Install Using apt Command Line
*   Google Chrome Install Using .deb

Microsoft Edge

*   Microsoft Edge Install Using apt Command Line
*   Microsoft Edge Install Using .deb

Opera

*   Opera Install Using Snap Store
*   Opera Install Using snap Command Line

Librewolf

*   Librewolf Install Using Software Manager
*   Librewolf Install Using apt Command Line
*   Librewolf Install Using flatpak Command Line

Pale Moon

*   Pale Moon Install Using apt Command Line

Firefox

Firefox Install Using Software Manager

![](Images/image00862.jpeg)

Open, Software Manager

Type In,

firefox

Click, Firefox

Click, Install

Firefox Install Using apt Command Line

![](Images/image00863.jpeg)

Open, Terminal

Type In,

sudo apt install firefox

Press, Enter

Firefox Install Using flatpak Command Line

![](Images/image00864.jpeg)

Open, Terminal

Type In,

flatpak install flathub org.mozilla.firefox

Press, Enter

Firefox Install Using Snap Store

![](Images/image00865.jpeg)

Open, Snap Store

Type In,

firefox

Click, Firefox

Click, Install

Firefox Install Using snap Command Line

![](Images/image00866.jpeg)

Open, Terminal

Type In,

sudo snap install firefox

Press, Enter

Firefox ESR

Firefox ESR Install Using .tar.gz

![](Images/image00867.jpeg)

Go to,

[https://www.mozilla.org/en-GB/firefox/all/#product-desktop-esr](https://www.mozilla.org/en-GB/firefox/all/#product-desktop-esr)

Select, Firefox Extended Support Release, 91.12.0esr, Linux 64-bit, English

Click, Download now to Download firefox-91.12.0esr.tar.bz2

Go to, Where firefox-91.12.0esr.tar.bz2 is Downloaded

Double Click, firefox-91.12.0esr.tar.bz2

Extract, To ~/Applications

Go to, Where firefox is extracted

Double Click, Firefox

Double Click, Firefox

Chromium

Chromium Install Using Snap Store

![](Images/image00868.jpeg)

Open, Snap Store

Type In,

chromium

Click, chromium

Click, Install

Chromium Install Using snap Command Line

![](Images/image00869.jpeg)

Open, Terminal

Type In,

sudo snap install chromium

Press, Enter

Google Chrome

Google Chrome Install Using apt Command Line

![](Images/image00870.jpeg)

Open, Terminal

Type In,

wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -

Press, Enter

![](Images/image00871.jpeg)

Type In,

sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'

Press, Enter

![](Images/image00872.jpeg)

Type In,

sudo apt update && sudo apt install google-chrome-stable

Press, Enter

Google Chrome Install Using .deb

![](Images/image00873.jpeg)

Go to,

[https://www.google.com/intl/en_uk/chrome/](https://www.google.com/intl/en_uk/chrome/)

Click, Download Chrome

Dot, Circle in the same row as 64 bit .deb (for Debian/Ubuntu)

Click, Accept and install to Download google-chrome-stable_current_amd64.deb

Go to, Where google-chrome-stable_current_amd64.deb is Downloaded

Double Click, google-chrome-stable_current_amd64.deb

Click, Install

Microsoft Edge

Microsoft Edge Install Using apt Command Line

![](Images/image00874.jpeg)

Open, Terminal

Type In,

  sudo sh -c 'echo "deb [arch=amd64] http://packages.microsoft.com/repos/edge/ stable main" >> /etc/apt/sources.list.d/microsoft_edge.list'

Press, Enter

![](Images/image00875.jpeg)

Type In,

sudo apt update && sudo apt install microsoft-edge-stable

Press, Enter

Microsoft Edge Install Using .deb

![](Images/image00876.jpeg)

Go to,

[https://www.microsoft.com/en-us/edge](https://www.microsoft.com/en-us/edge)

Click, DOWNLOAD for linux

Click, Linux (.deb)

Click, Accept and download to Download microsoft-edge-stable_103.0.1264.77-1_amd64.deb

Go to, Where microsoft-edge-stable_103.0.1264.77-1_amd64.deb is Downloaded

Double Click, microsoft-edge-stable_103.0.1264.77-1_amd64.deb

Click, Install

Opera

Opera Install Using Snap Store

![](Images/image00877.jpeg)

Open, Snap Store

Type In,

opera

Click, opera

Click, Install

Opera Install Using snap Command Line

![](Images/image00878.jpeg)

Open, Terminal

Type In,

sudo snap install opera

Press, Enter

Librewolf

Librewolf Install Using Software Manager

![](Images/image00879.jpeg)

Open, Software Manager

Type In,

librewolf

Click, Librewolf

Click, Install

Librewolf Install Using apt Command Line

![](Images/image00880.jpeg)

Open, Terminal

Type In,

distro=$(if echo " bullseye focal impish jammy uma una vanessa " | grep -q " $(lsb_release -sc) "; then echo $(lsb_release -sc); else echo focal; fi)

Press, Enter

![](Images/image00881.jpeg)

Type In,

wget -O- https://deb.librewolf.net/keyring.gpg | sudo gpg --dearmor -o /usr/share/keyrings/librewolf.gpg

Press, Enter

![](Images/image00882.jpeg)

Type In,

sudo tee /etc/apt/sources.list.d/librewolf.sources << EOF > /dev/null

Press, Enter

![](Images/image00883.jpeg)

Type In,

sudo apt update && sudo apt install librewolf

Press, Enter

Librewolf Install Using flatpak Command Line

![](Images/image00884.jpeg)

Open, Terminal

Type In,

flatpak install flathub io.gitlab.librewolf-community

Press, Enter

Pale Moon

Pale Moon Install Using apt Command Line

![](Images/image00885.jpeg)

Open, Terminal

Type In,

echo 'deb http://download.opensuse.org/repositories/home:/stevenpusser/xUbuntu_22.04/ /' | sudo tee /etc/apt/sources.list.d/home:stevenpusser.list

Press, Enter

![](Images/image00886.jpeg)

Type In,

curl -fsSL https://download.opensuse.org/repositories/home:stevenpusser/xUbuntu_22.04/Release.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/home_stevenpusser.gpg > /dev/null

Press, Enter

![](Images/image00887.jpeg)

Type In,

sudo apt update && sudo apt install palemoon

Press, Enter

World of Warcraft

World of Warcraft is an MMORPG that works rather well under Linux Mint 21, through lutris and wine (with DXVK and VKD3D Installed), with optimizations given here, such as,

*   Possible Fix for Dark Screen In-Game Store Bug
*   Direct X 12 Error
*   How To Manually Install World of Warcraft Addons

Possible Fix for Dark Screen In-Game Store Bug

![](Images/image00888.jpeg)

Open, Terminal

Type In,

winecfg

Press, Enter

Click, Install

![](Images/image00889.jpeg)

Click, Box in the same row as Windows Version

Click, Windows 10

Click, Apply

Click, Staging

![](Images/image00890.jpeg)

Tick, Boxes in the same rows as,

*   Enable CSMT for better graphic performance
*   Enable VAAPI as backend for DXVA2 GPU decoding

Click, Apply

Click, Drives

![](Images/image00891.jpeg)

Click, Add..

Select, Drive Letter

Click, OK

![](Images/image00892.jpeg)

Under, Drive configuration

Select, Newly Created Drive Letter (e.g. D:)

Click, Browse

![](Images/image00893.jpeg)

Expand, mnt, By, Clicking the + in the same row

![](Images/image00894.jpeg)

Expand, Drive where World of Warcraft is located, By, Clicking + in the same row

Select, World of Warcraft folder

Click, OK

Click, Apply

Click OK

Direct X 12 Error

![](Images/image00895.jpeg)

Open, Lutris

Select, Blizzard Battle.net

Right Click, Blizzard Battle.net

Click, Configure

![](Images/image00896.jpeg)

Click, Runner options

Click, Show Advanced Options

Move, Switches, to the LEFT in the same rows as,

*   Enable VKD3D
*   Enable DXVK-NVAPI / DLSS
*   Enable AMD FidelityFX Super Resolution (FSR)
*   Enable BattleEye Anti-Cheat
*   Enable Easy Anti-Cheat

I would personally leave other options as default.

How To Manually Install World of Warcraft Addons

![](Images/image00897.jpeg)

Go to,

[https://www.curseforge.com/wow/addons](https://www.curseforge.com/wow/addons)

Type In,

comix

Press, Enter

Click, Comix Reborn

![](Images/image00898.jpeg)

Under, Recent Files, and Under WoW, Click, Downwards Arrow, in the same row as, v9.2.0.0-release to Download Comix-v9.2.0.0-release.zip

Double Click, Comix-v9.2.0.0-release.zip

![](Images/image00899.jpeg)

Select, Comix

Extract, To World of Warcraft/_retail_/Interface/AddOns

or World of Warcraft/_classic_/Interface/AddOns for Wrath of The Lich King Classic

or World of Warcraft/_classic_era_/Interface/AddOns for World of Warcraft Classic Era

World of Warcraft Addon Managers

World Of Warcraft Addon Managers greatly ease the process of searching for , managing, installing and updating World of Warcraft Addons, and come with features such as,

*   Installing addons from sources, such as Curseforge
*   Updating all or individual addons
*   Removing addons

This chapter covers,

Curseforge

*   Curseforge Install Using .AppImage
*   Curseforge Manually Add Game
*   Curseforge Install Addon
*   Curseforge Update Addon
*   Curseforge Remove Addon

Curseforge

Curseforge Install Using .AppImage

![](Images/image00900.jpeg)

Go to,

https://download.curseforge.com/

Click, Download (WoW only) to Download curseforge-latest-linux.zip

Go to, Where curseforge-latest-linux is Downloaded

Double Click, curseforge-latest-linux

Select, Curseforge AppImage

Extract, To ~/Downloads

Go to, Where Curseforge AppImage is Extracted

Double Click, Curseforge AppImage

Click, Integrate and Run

Curseforge Manually Add Game

![](Images/image00901.jpeg)

Open, Curseforge

Click, 3 Vertical dots Icon

Click, Manually add a game

Select. World of Warcraft/_retail_

or _classic_ for WOTLK Classic

or _classic_era_ for World of Warcraft Vanilla Classic

Curseforge Install Addon

![](Images/image00902.jpeg)

Open, Curseforge

Click, Get More Addons

Click, Search Bar

Type In,

comix

Click, Install, In the same row as Comix Reborn

Curseforge Update Addon

![](Images/image00903.jpeg)

Open, Curseforge

Click, My Addons

Click, Update All

Curseforge Remove Addon

![](Images/image00904.jpeg)

Open, Curseforge

Right Click, Comix

Click, Delete Addon

About The Author

The Author of this self-help learning book graduated from The University of Buckingham with a degree in Business and Communications and now lives in the family home in the United Kingdom.

This is the authors seventeenth literary work with additional material in the planning stages, with subsequent works that hope to make beings and organizations happier.

Bibliography

The books written by the author, with the most recent going first:

*   Linux Mint 21 ‘Vanessa’ After Install Self Help Guide, 2022
*   Ubuntu 18.04 LTS After Install Self Help Guide, 2022
*   Pop!_OS 22.04 LTS After Install Self Help Guide, 2022
*   Ubuntu 22.04 LTS After Install Self Help Guide, 2022
*   Create An OS - With Cubics and Ubuntu 20.04 LTS, 2022
*   LMDE 5 Elise After Install Self Help Guide, 2022
*   Linux Mint 20.03 Self Help After Install Guide, 2022
*   Windows 11 After Install Self Help Guide, 2022
*   openSUSE Tumbleweed After Install Self Help Guide, 2022
*   Debian 11 Bullseye After Install Self Help Guide Remastered, 2021
*   Ubuntu 20.04 LTS Self Help Guide Remastered, 2021
*   Linux Mint 20.XX Self Help Guide, 2021
*   Pop OS 20.04 Self Help Guide, 2021
*   Debian 11 Augment Self Help Guide, 2021
*   Ubuntu 20.04 LTS After Install Augment Self Help Guide, 2021
*   Debian 11 After Install Self Help Guide, 2021
*   Ubuntu 20.04.03 LTS After Install Self Help Guide, 2021