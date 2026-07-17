![](Images/cover01183.jpeg)

![](Images/image00746.jpeg)

Copyright

First published on Amazon.co.uk by Morgan Partridge in 2022

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

Linux Mark Institute and the community, for developing and maintaining Linux Mint.

Blizzard for developing and publishing World of Warcraft that I really love and enjoy.

WINE or Wine Is Not An Emulator for the compatibility layer.

Lutris making it far more accessible to Install and play games and software.

Gabe Newell and Valve for developing and publishing the Steam Store.

Install Machine Details

All details of this self help learning guide has been undertaken on bare metal or directly on hardware, rather than a virtual machine

The Install of Linux Mint 20.03 has been done on a manually partitioned drive with:

53 GB for the / or root partition

20 GB for the swap partition

I have used the existing EFI partition from the Ubuntu 20.04.03 LTS Install

The specifications of the computer used to Install Linux Mint 20.03 are:

CPU: Intel(R)Core(TM) i3-9100F CPU

RAM or Memory: 16GB DDR4

Motherboard: MSI B365M PRO-VH REV 1.0

GPU or Graphics Card: MSI Nvidia 1060 GTX 6GB

Monitor: 24" HP 24o Monitor

SSD: 1618 GB Over Samsung, PNY and SPCC Drives

HDD Internal: 9TB over 2 Western Digital Drives

HDD External: 1TB JMicron

Soundcard: USB 3.0 External Phoinkas Soundcard

Speakers: Amazon Basics 2.0 Speakers

Headphones: Generic 2.0 Earphones

Headset: Kingston HyperX Cloud Alpha 3.5 MM

Keyboard 1 & 2: USB 2.0 Generic Mini Gaming Keyboard, USB 2.0 Basic Full Sized Keyboard

Mouse: USB 2.0 HP Wireless Mouse X200, USB 2.0 Basic Wired Mouse

Network: USB 3.0 Realtek Gigabit Adapter, Realtek Motherboard Gigabit PCI Port

Phone: Samsung Smartphone

USB Hub: USB 3.0 External Phoinkas Soundcard

Printer: Epson Network Printer

Introduction

This guide was written to be a Self Help Guide for Linux Mint 20.03

To increase your security you will be required to ENTER your password to complete most steps on this list so be sure to have it at hand

After typing in all sudo commands and your password you may be required to confirm by pressing ENTER to continue or ESC to abort

Make sure you update and upgrade your Linux Mint 20.03 every day a few days or as you like to ensure security and stability

Do not ever use sudo apt auto remove as it could destabilize or break Linux Mint 20.03

You should type in what is stated to help you to remember but you can copy and paste if you wish

Make sure to click Keep or Save File when downloading the .deb, .appimage, jar, .targz, .taxxz and other files.

Table of Contents

[​ Copyright             2](#part0001.xhtml___RefHeading___Toc3588_2208911920)

[​ Disclaimer             3](#part0002.xhtml___RefHeading___Toc3590_2208911920)

[​ Trademark             4](#part0003.xhtml___RefHeading___Toc3592_2208911920)

[​ Acknowledgements             5](#part0004.xhtml___RefHeading___Toc3594_2208911920)

[​ Install Machine Details             6](#part0005.xhtml___RefHeading___Toc3596_2208911920)

[​ Introduction             7](#part0006.xhtml___RefHeading___Toc3598_2208911920)

[​ Audio Editors             13](#part0008.xhtml___RefHeading___Toc3600_2208911920)

[​ Ardour             14](#part0009.xhtml___RefHeading___Toc3602_2208911920)

[​ Audacity             17](#part0012.xhtml___RefHeading___Toc3604_2208911920)

[​ Kwave             23](#part0018.xhtml___RefHeading___Toc3606_2208911920)

[​ Cloud Backup             29](#part0024.xhtml___RefHeading___Toc3608_2208911920)

[​ Insync             30](#part0025.xhtml___RefHeading___Toc3610_2208911920)

[​ overGrive             32](#part0027.xhtml___RefHeading___Toc3612_2208911920)

[​ Cloud Office Suites             34](#part0029.xhtml___RefHeading___Toc3614_2208911920)

[​ Google Docs             35](#part0030.xhtml___RefHeading___Toc3616_2208911920)

[​ Microsoft Office 365             36](#part0031.xhtml___RefHeading___Toc3618_2208911920)

[​ Zoho Docs             37](#part0032.xhtml___RefHeading___Toc3620_2208911920)

[​ Communication             38](#part0033.xhtml___RefHeading___Toc3622_2208911920)

[​ Discord             39](#part0034.xhtml___RefHeading___Toc3624_2208911920)

[​ Pidgin             42](#part0037.xhtml___RefHeading___Toc3626_2208911920)

[​ Telegram             45](#part0040.xhtml___RefHeading___Toc3628_2208911920)

[​ Compatibility Layers             48](#part0043.xhtml___RefHeading___Toc3630_2208911920)

[​ Anbox             49](#part0044.xhtml___RefHeading___Toc3632_2208911920)

[​ WINE Staging             51](#part0046.xhtml___RefHeading___Toc3634_2208911920)

[​ Cryptocurrency Wallets             57](#part0052.xhtml___RefHeading___Toc3636_2208911920)

[​ Bitcoin-Core             58](#part0053.xhtml___RefHeading___Toc3638_2208911920)

[​ Coin Wallet             61](#part0056.xhtml___RefHeading___Toc3640_2208911920)

[​ Electrum             64](#part0059.xhtml___RefHeading___Toc3642_2208911920)

[​ Data Recovery             67](#part0062.xhtml___RefHeading___Toc3644_2208911920)

[​ R-Linux             68](#part0063.xhtml___RefHeading___Toc3646_2208911920)

[​ Desktop Environments             70](#part0065.xhtml___RefHeading___Toc3648_2208911920)

[​ Cinnamon             71](#part0066.xhtml___RefHeading___Toc3650_2208911920)

[​ Gnome             72](#part0067.xhtml___RefHeading___Toc3652_2208911920)

[​ KDE Plasma             73](#part0068.xhtml___RefHeading___Toc3654_2208911920)

[​ Tasksel             76](#part0071.xhtml___RefHeading___Toc3656_2208911920)

[​ Ubuntu Desktop             77](#part0072.xhtml___RefHeading___Toc3658_2208911920)

[​ Download Managers             79](#part0074.xhtml___RefHeading___Toc3660_2208911920)

[FireDM             80](#part0075.xhtml___RefHeading___Toc3662_2208911920)

[​ KGet             82](#part0077.xhtml___RefHeading___Toc3682_2208911920)

[​ uGet             85](#part0080.xhtml___RefHeading___Toc3684_2208911920)

[​ Ebook Readers             91](#part0086.xhtml___RefHeading___Toc3686_2208911920)

[​ Calibre             92](#part0087.xhtml___RefHeading___Toc3688_2208911920)

[​ Fbreader             97](#part0092.xhtml___RefHeading___Toc3690_2208911920)

[​ Lucidor             103](#part0098.xhtml___RefHeading___Toc3692_2208911920)

[​ Elder Gaming             105](#part0100.xhtml___RefHeading___Toc3694_2208911920)

[​ Dosbox             106](#part0101.xhtml___RefHeading___Toc3696_2208911920)

[​ ResidualVM             112](#part0107.xhtml___RefHeading___Toc3698_2208911920)

[​ ScummVM             118](#part0113.xhtml___RefHeading___Toc3700_2208911920)

[​ File Compression and Extraction             124](#part0119.xhtml___RefHeading___Toc3702_2208911920)

[​ Engrampa             125](#part0120.xhtml___RefHeading___Toc3704_2208911920)

[​ p7zip-desktop             128](#part0123.xhtml___RefHeading___Toc3706_2208911920)

[​ PeaZip             131](#part0126.xhtml___RefHeading___Toc3708_2208911920)

[​ Image Editors             133](#part0128.xhtml___RefHeading___Toc3710_2208911920)

[​ Blender             134](#part0129.xhtml___RefHeading___Toc3712_2208911920)

[​ GIMP or Gnu Image Manipulation Program             140](#part0135.xhtml___RefHeading___Toc3714_2208911920)

[​ Krita             146](#part0141.xhtml___RefHeading___Toc3716_2208911920)

[​ Pinta             152](#part0147.xhtml___RefHeading___Toc3718_2208911920)

[​ Inkscape             158](#part0153.xhtml___RefHeading___Toc3720_2208911920)

[​ Internet Video Broadcasting             164](#part0159.xhtml___RefHeading___Toc3722_2208911920)

[​ OBS Studio             165](#part0160.xhtml___RefHeading___Toc3724_2208911920)

[​ Media Player             175](#part0170.xhtml___RefHeading___Toc3726_2208911920)

[​ Parole             176](#part0171.xhtml___RefHeading___Toc3728_2208911920)

[​ SMPlayer             179](#part0174.xhtml___RefHeading___Toc3730_2208911920)

[​ VLC             182](#part0177.xhtml___RefHeading___Toc3732_2208911920)

[​ Modern Gaming             188](#part0183.xhtml___RefHeading___Toc3734_2208911920)

[Blizzard Battle.net             189](#part0184.xhtml___RefHeading___Toc3736_2208911920)

[​ Lutris             196](#part0191.xhtml___RefHeading___Toc3738_2208911920)

[​ Proton-QT             199](#part0194.xhtml___RefHeading___Toc3740_2208911920)

[​ Steam             201](#part0196.xhtml___RefHeading___Toc3742_2208911920)

[​ WINE             204](#part0199.xhtml___RefHeading___Toc3744_2208911920)

[​ Music On Demand Streaming             210](#part0205.xhtml___RefHeading___Toc3746_2208911920)

[​ Amazon Music             211](#part0206.xhtml___RefHeading___Toc3748_2208911920)

[​ Apple Music             212](#part0207.xhtml___RefHeading___Toc3750_2208911920)

[​ Spotify             213](#part0208.xhtml___RefHeading___Toc3752_2208911920)

[​ Spotify Client             214](#part0209.xhtml___RefHeading___Toc3754_2208911920)

[​ Tidal Access Using Website             216](#part0211.xhtml___RefHeading___Toc3756_2208911920)

[​ Youtube Music             217](#part0212.xhtml___RefHeading___Toc3758_2208911920)

[Music Players             219](#part0213.xhtml___RefHeading___Toc3760_2208911920)

[Audacious             220](#part0214.xhtml___RefHeading___Toc3762_2208911920)

[Clementine             223](#part0217.xhtml___RefHeading___Toc3764_2208911920)

[​ DeaDBeeF             229](#part0223.xhtml___RefHeading___Toc3766_2208911920)

[​ Office Suites             232](#part0226.xhtml___RefHeading___Toc3768_2208911920)

[​ LibreOffice             233](#part0227.xhtml___RefHeading___Toc3770_2208911920)

[​ ONLYOFFICE Desktop Editors             239](#part0233.xhtml___RefHeading___Toc3772_2208911920)

[​ OpenOffice             244](#part0238.xhtml___RefHeading___Toc3774_2208911920)

[​ SoftMaker FreeOffice             246](#part0240.xhtml___RefHeading___Toc3776_2208911920)

[​ WPS Office             248](#part0242.xhtml___RefHeading___Toc3778_2208911920)

[​ PDF Readers             250](#part0244.xhtml___RefHeading___Toc3780_2208911920)

[​ Evince             251](#part0245.xhtml___RefHeading___Toc3782_2208911920)

[​ Okular             257](#part0251.xhtml___RefHeading___Toc3784_2208911920)

[​ Remote Working             264](#part0257.xhtml___RefHeading___Toc3786_2208911920)

[​ Citrix Workspace             265](#part0258.xhtml___RefHeading___Toc3788_2208911920)

[​ Microsoft Teams             267](#part0260.xhtml___RefHeading___Toc3790_2208911920)

[​ Zoom             269](#part0262.xhtml___RefHeading___Toc3792_2208911920)

[​ Security             273](#part0266.xhtml___RefHeading___Toc3794_2208911920)

[All Of The Firewall Ports I Use             274](#part0267.xhtml___RefHeading___Toc3796_2208911920)

[TCP Ports With Spaces             274](#part0267.xhtml___RefHeading___Toc3798_2208911920)

[TCP Ports Without Spaces             274](#part0267.xhtml___RefHeading___Toc3800_2208911920)

[UDP Ports With Spaces             274](#part0267.xhtml___RefHeading___Toc3802_2208911920)

[UDP Ports Without Spaces             274](#part0267.xhtml___RefHeading___Toc3804_2208911920)

[​ Bitwarden             275](#part0268.xhtml___RefHeading___Toc3806_2208911920)

[​ Buttercup             278](#part0271.xhtml___RefHeading___Toc3808_2208911920)

[​ ClamAV             280](#part0273.xhtml___RefHeading___Toc3810_2208911920)

[​ ClamAV Realtime             281](#part0274.xhtml___RefHeading___Toc3812_2208911920)

[​ ClamTK             284](#part0277.xhtml___RefHeading___Toc3814_2208911920)

[​ ClamTK Right Click To Scan             287](#part0280.xhtml___RefHeading___Toc3816_2208911920)

[​ Firetools             290](#part0283.xhtml___RefHeading___Toc3818_2208911920)

[​ Firejail             293](#part0286.xhtml___RefHeading___Toc3820_2208911920)

[​ GUFW             296](#part0289.xhtml___RefHeading___Toc3822_2208911920)

[GUFW Set Multi Port Rules             299](#part0292.xhtml___RefHeading___Toc3824_2208911920)

[​ GUFW Set Range Port Rules             300](#part0293.xhtml___RefHeading___Toc3826_2208911920)

[​ GUFW Set Single Port Rules             301](#part0294.xhtml___RefHeading___Toc3828_2208911920)

[​ UFW             302](#part0295.xhtml___RefHeading___Toc3830_2208911920)

[​ UFW Set Multi and Range Port Rules             303](#part0296.xhtml___RefHeading___Toc3832_2208911920)

[​ UFW Set Multi Port Rules             304](#part0297.xhtml___RefHeading___Toc3834_2208911920)

[​ UFW Set Range Port Rules             305](#part0298.xhtml___RefHeading___Toc3836_2208911920)

[​ UFW Set Single Port Rules             306](#part0299.xhtml___RefHeading___Toc3838_2208911920)

[​ Software Distribution             307](#part0300.xhtml___RefHeading___Toc3840_2208911920)

[​ AppImageLauncher             308](#part0301.xhtml___RefHeading___Toc3842_2208911920)

[​ Flathub             311](#part0304.xhtml___RefHeading___Toc3844_2208911920)

[​ Flatpak             312](#part0305.xhtml___RefHeading___Toc3846_2208911920)

[​ Java JRE JDK             314](#part0307.xhtml___RefHeading___Toc3848_2208911920)

[​ Snap             316](#part0308.xhtml___RefHeading___Toc3850_2208911920)

[​ Snap Store             319](#part0311.xhtml___RefHeading___Toc3852_2208911920)

[​ System Settings             320](#part0312.xhtml___RefHeading___Toc3854_2208911920)

[​ Alt-Tab Thumbnails             321](#part0313.xhtml___RefHeading___Toc3856_2208911920)

[​ AMD Drivers             322](#part0314.xhtml___RefHeading___Toc3858_2208911920)

[​ Auto Mount Disks             331](#part0322.xhtml___RefHeading___Toc3860_2208911920)

[​ Changing Kernel Versions             334](#part0325.xhtml___RefHeading___Toc3862_2208911920)

[​ Changing Mouse Acceleration             338](#part0329.xhtml___RefHeading___Toc3864_2208911920)

[​ Changing Sound Device             339](#part0330.xhtml___RefHeading___Toc3866_2208911920)

[​ Changing Themes             340](#part0331.xhtml___RefHeading___Toc3868_2208911920)

[​ Enable LibreOffice Night Mode             341](#part0332.xhtml___RefHeading___Toc3870_2208911920)

[​ How To Block Websites Using Xed             342](#part0333.xhtml___RefHeading___Toc3872_2208911920)

[​ libopusfile0             344](#part0335.xhtml___RefHeading___Toc3874_2208911920)

[​ Nautilus File Manager             345](#part0336.xhtml___RefHeading___Toc3876_2208911920)

[​ Night Light             348](#part0339.xhtml___RefHeading___Toc3878_2208911920)

[​ Nvidia Drivers             349](#part0340.xhtml___RefHeading___Toc3880_2208911920)

[​ Possible Intel Sound Crackle Fix             352](#part0343.xhtml___RefHeading___Toc3882_2208911920)

[​ Possible Parole Segmentation Fault Fix             353](#part0344.xhtml___RefHeading___Toc3884_2208911920)

[​ Set As Default For File Type             354](#part0345.xhtml___RefHeading___Toc3886_2208911920)

[​ Setting Alternative DNS             355](#part0346.xhtml___RefHeading___Toc3888_2208911920)

[​ Startup Applications             360](#part0351.xhtml___RefHeading___Toc3890_2208911920)

[​ Updating System             364](#part0355.xhtml___RefHeading___Toc3892_2208911920)

[​ System Utilities             370](#part0361.xhtml___RefHeading___Toc3894_2208911920)

[​ Bleachbit             371](#part0362.xhtml___RefHeading___Toc3896_2208911920)

[​ Boot Repair             374](#part0365.xhtml___RefHeading___Toc3898_2208911920)

[​ Czkawka             376](#part0367.xhtml___RefHeading___Toc3900_2208911920)

[​ GParted             379](#part0370.xhtml___RefHeading___Toc3902_2208911920)

[​ gpustat             382](#part0373.xhtml___RefHeading___Toc3904_2208911920)

[​ Grub Customizer             383](#part0374.xhtml___RefHeading___Toc3906_2208911920)

[​ HardInfo             385](#part0376.xhtml___RefHeading___Toc3908_2208911920)

[​ K4DirStat             388](#part0379.xhtml___RefHeading___Toc3910_2208911920)

[​ KDE Partition Manager             391](#part0382.xhtml___RefHeading___Toc3912_2208911920)

[​ Neofetch             395](#part0385.xhtml___RefHeading___Toc3914_2208911920)

[​ Psensor             397](#part0387.xhtml___RefHeading___Toc3916_2208911920)

[​ QDirStat             401](#part0391.xhtml___RefHeading___Toc3918_2208911920)

[​ Stacer             402](#part0392.xhtml___RefHeading___Toc3920_2208911920)

[​ Sweeper             405](#part0395.xhtml___RefHeading___Toc3922_2208911920)

[​ Video Editors             411](#part0401.xhtml___RefHeading___Toc3924_2208911920)

[​ Kdenlive             412](#part0402.xhtml___RefHeading___Toc3926_2208911920)

[​ Openshot             418](#part0408.xhtml___RefHeading___Toc3928_2208911920)

[​ Shotcut             421](#part0411.xhtml___RefHeading___Toc3930_2208911920)

[​ Video On Demand Streaming             427](#part0417.xhtml___RefHeading___Toc3932_2208911920)

[​ Amazon Prime Video             428](#part0418.xhtml___RefHeading___Toc3934_2208911920)

[​ Disney+             429](#part0419.xhtml___RefHeading___Toc3936_2208911920)

[​ Netflix             430](#part0420.xhtml___RefHeading___Toc3938_2208911920)

[​ Virtualization             431](#part0421.xhtml___RefHeading___Toc3940_2208911920)

[​ Virt-Manager             432](#part0422.xhtml___RefHeading___Toc3942_2208911920)

[​ Virtualbox             433](#part0423.xhtml___RefHeading___Toc3944_2208911920)

[​ Virtualbox Extension Pack             437](#part0427.xhtml___RefHeading___Toc3946_2208911920)

[​ Web Browsers             440](#part0430.xhtml___RefHeading___Toc3948_2208911920)

[​ Chromium             441](#part0431.xhtml___RefHeading___Toc3950_2208911920)

[​ Firefox ESR             444](#part0434.xhtml___RefHeading___Toc3952_2208911920)

[​ Google Chrome             447](#part0437.xhtml___RefHeading___Toc3954_2208911920)

[​ Microsoft Edge             449](#part0439.xhtml___RefHeading___Toc3956_2208911920)

[​ Opera             452](#part0442.xhtml___RefHeading___Toc3958_2208911920)

[​ World of Warcraft             455](#part0445.xhtml___RefHeading___Toc3960_2208911920)

[Battle.net Launch Arguments             456](#part0446.xhtml___RefHeading___Toc3962_2208911920)

[​ In-Game Store Lutris Black Screen Fix             457](#part0447.xhtml___RefHeading___Toc3964_2208911920)

[​ In-Game Store WINE Black Screen Fix             464](#part0453.xhtml___RefHeading___Toc3966_2208911920)

[​ Lutris Battle.net Runner and System Options             472](#part0461.xhtml___RefHeading___Toc3968_2208911920)

[​ Manually Installing World of Warcraft Addons             474](#part0463.xhtml___RefHeading___Toc3970_2208911920)

[​ World of Warcraft Addon Managers             475](#part0464.xhtml___RefHeading___Toc3972_2208911920)

[​ Ajour             476](#part0465.xhtml___RefHeading___Toc3974_2208911920)

[​ Ajour Delete Addon             478](#part0467.xhtml___RefHeading___Toc3976_2208911920)

[​ Ajour Delete Variable             480](#part0469.xhtml___RefHeading___Toc3978_2208911920)

[​ Ajour Install Addon             482](#part0471.xhtml___RefHeading___Toc3980_2208911920)

[​ Ajour New Addon Directory             483](#part0472.xhtml___RefHeading___Toc3982_2208911920)

[​ Strongbox             485](#part0474.xhtml___RefHeading___Toc3984_2208911920)

[​ Strongbox Change Theme             487](#part0476.xhtml___RefHeading___Toc3986_2208911920)

[​ Strongbox Delete Addon             488](#part0477.xhtml___RefHeading___Toc3988_2208911920)

[​ Strongbox Delete Multiple Addons             489](#part0478.xhtml___RefHeading___Toc3990_2208911920)

[​ Strongbox Install Addon             491](#part0479.xhtml___RefHeading___Toc3992_2208911920)

[​ Strongbox Install Multiple Addons             492](#part0480.xhtml___RefHeading___Toc3994_2208911920)

[​ Strongbox New Addon Directory             493](#part0481.xhtml___RefHeading___Toc3996_2208911920)

[​ wowmatrix             495](#part0483.xhtml___RefHeading___Toc3998_2208911920)

[​ wowmatrix Delete Addon             498](#part0486.xhtml___RefHeading___Toc4000_2208911920)

[​ wowmatrix Delete Multiple Addons             500](#part0488.xhtml___RefHeading___Toc4002_2208911920)

[​ wowmatrix Install Addon             501](#part0489.xhtml___RefHeading___Toc4004_2208911920)

[​ wowmatrix New Addon Directory             502](#part0490.xhtml___RefHeading___Toc4006_2208911920)

[​ Wowup             504](#part0492.xhtml___RefHeading___Toc4008_2208911920)

[​ Wowup Delete Addon             506](#part0494.xhtml___RefHeading___Toc4010_2208911920)

[​ Wowup Delete Multiple Addons             508](#part0496.xhtml___RefHeading___Toc4012_2208911920)

[​ Wowup Install Addon             510](#part0498.xhtml___RefHeading___Toc4014_2208911920)

[​ Wowup New Addon Directory             512](#part0500.xhtml___RefHeading___Toc4016_2208911920)

[​ About The Author             514](#part0502.xhtml___RefHeading___Toc4018_2208911920)

[​ Bibliography             515](#part0503.xhtml___RefHeading___Toc4020_2208911920)

Audio Editors

Ardour

Audacity

Kwave

Ardour

![](Images/image00747.jpeg)

Open: Software Manager

Type In or Copy and Paste:

ardour

Click: Ardour

![](Images/image00748.jpeg)

Click: Install

![](Images/image00749.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install ardour

Press: ENTER

Audacity

![](Images/image00750.jpeg)

Open: Software Manager

Type In or Copy and Paste:

audacity

Click: Audacity

![](Images/image00751.jpeg)

Click: Install

![](Images/image00752.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install audacity

Press: ENTER

![](Images/image00753.jpeg)

Open: Snap Store

Type In or Copy and Paste:

audacity

Click: Audacity

![](Images/image00754.jpeg)

Click: Install

![](Images/image00755.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install audacity

Press: ENTER

Kwave

![](Images/image00756.jpeg)

Open: Software Manager

Type In or Copy and Paste:

kwave

Click: Kwave

![](Images/image00757.jpeg)

Click: Install

![](Images/image00758.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install kwave

Press: ENTER

![](Images/image00759.jpeg)

Open: Snap Store

Type In or Copy and Paste:

kwave

Click: kwave

![](Images/image00760.jpeg)

Click: Install

![](Images/image00761.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install kwave

Press: ENTER

Cloud Backup

*   Insync
*   overGrive

Insync

![](Images/image00762.jpeg)

Go to:

[https://www.insynchq.com/downloads](https://www.insynchq.com/downloads)

Click: Box under Installers

Click: Linux Mint

Click: Box under Installers and Packages

Click: 20.x

Click: Download

To: Download insync_3.7.1.50307-focal_amd64.deb

Go to: Where insync_3.7.1.50307-focal_amd64.deb is downloaded

Double Click: insync_3.7.1.50307-focal_amd64.deb

![](Images/image00763.jpeg)

Click: Install Package

overGrive

![](Images/image00764.jpeg)

Go to:

[https://www.thefanclub.co.za/overgrive](https://www.thefanclub.co.za/overgrive)

Click: overGrive 3.3.13 - Debian|Ubuntu|Mint

To: Download overgrive_3.3.13_all.deb

Go to: Where overgrive_3.3.13_all.deb is downloaded

Double Click: overgrive_3.3.13_all.deb

![](Images/image00765.jpeg)

Click: Install Package

Cloud Office Suites

*   Google Docs
*   Microsoft Office 365
*   Zoho Docs

Google Docs

![](Images/image00766.jpeg)

Open: Firefox

Go to:

[https://www.google.co.uk/docs/about/](https://www.google.co.uk/docs/about/)

Sign in to Access Google Docs

Microsoft Office 365

![](Images/image00767.jpeg)

Open: Firefox

Go to:

[https://www.office.com/](https://www.office.com/)

Sign in to Access

Zoho Docs

![](Images/image00768.jpeg)

Open: Firefox

Go to:

[https://www.zoho.com/docs/](https://www.zoho.com/docs/)

Sign in to Access

Communication

Discord

Pidgin

Telegram

Discord

![](Images/image00769.jpeg)

Open: Snap Store

Type In or Copy and Paste:

discord

Click: Discord

![](Images/image00770.jpeg)

Click: Install

![](Images/image00771.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install discord

Press: ENTER

Pidgin

![](Images/image00772.jpeg)

Open: Software Manager

Type In or Copy and Paste:

pidgin

Click:  Pidgin

![](Images/image00773.jpeg)

Click: Install

![](Images/image00774.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install pidgin

Press: ENTER

Telegram

![](Images/image00775.jpeg)

Open: Snap Store

Type In or Copy and Paste:

telegram

Click: telegram-desktop

![](Images/image00776.jpeg)

Click: Install

![](Images/image00777.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install telegram-desktop

Press: ENTER

Compatibility Layers

Anbox

WINE Staging

Anbox

![](Images/image00778.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install --devmode --beta anbox

Press: ENTER

![](Images/image00779.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap refresh --beta --devmode anbox

Press: ENTER

To: Update Anbox

WINE Staging

![](Images/image00780.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo dpkg --add-architecture i386

Press: ENTER

![](Images/image00781.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image00782.jpeg)

Open: Terminal

Type In or Copy and Paste:

wget -qO- https://dl.winehq.org/wine-builds/winehq.key | sudo apt-key add -

Press: ENTER

![](Images/image00783.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt-add-repository 'deb http://dl.winehq.org/wine-builds/ubuntu/ bionic main'

Press: ENTER

![](Images/image00784.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image00785.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt-get install --install-recommends winehq-staging

Press: ENTER

Cryptocurrency Wallets

Bitcoin-Core

Coin Wallet

Electrum

Bitcoin-Core

![](Images/image00786.jpeg)

Open: Snap Store

Type In or Copy and Paste:

bitcoin-core

Click: bitcoin-core

![](Images/image00787.jpeg)

Click: Install

![](Images/image00788.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install bitcoin-core

Press: ENTER

Coin Wallet

![](Images/image00789.jpeg)

Open: Snap Store

Type In or Copy and Paste:

coin wallet

Click: Coin Wallet

![](Images/image00790.jpeg)

Click: Install

![](Images/image00791.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install coin-wallet

Press: ENTER

Electrum

![](Images/image00792.jpeg)

Open: Snap Store

Type In or Copy and Paste:

electrum

Click: electrum

![](Images/image00793.jpeg)

Click: Install

![](Images/image00794.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install electrum

Press: ENTER

Data Recovery

R-Linux

R-Linux

![](Images/image00795.jpeg)

Go to:

[https://www.r-studio.com/free-linux-recovery/Download.shtml](https://www.r-studio.com/free-linux-recovery/Download.shtml)

Click: Download Now in the same row as R-Linux for Debian/Ubuntu Linux platform (64-bit)

To: Download RLinux5_x64.deb

Go to: Where RLinux5_x64.deb is downloaded

Double Click: RLinux5_x64.deb

![](Images/image00796.jpeg)

Click: Install Package

Desktop Environments

Cinnamon

Gnome

KDE Plasma

Tasksel

Ubuntu Desktop

Cinnamon

![](Images/image00797.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install cinnamon

Press: ENTER

Gnome

![](Images/image00798.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install gnome

Press: ENTER

KDE Plasma

![](Images/image00799.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo add-apt-repository ppa:kubuntu-ppa/backports

Press: ENTER

![](Images/image00784.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image00800.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install kde-plasma-desktop

Press: ENTER

Tasksel

![](Images/image00801.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install tasksel

Press: ENTER

Ubuntu Desktop

![](Images/image00802.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo tasksel

Press: ENTER

![](Images/image00803.jpeg)

Use the Up and Down Arrow Keys to Navigate to Ubuntu desktop

Select: Ubuntu desktop by Pressing Space

Press: TAB until OK is selected

Press: ENTER

Download Managers

FireDM

KGet

uGet

FireDM

![](Images/image00804.jpeg)

Go to:

[https://github.com/firedm/FireDM/releases](https://github.com/firedm/FireDM/releases)

Click: FireDM-2022.2.5-x86_64.AppImage

To: Download FireDM-2022.2.5-x86_64.AppImage

Go to: Where FireDM-2022.2.5-x86_64.AppImage is downloaded

Double Click: FireDM-2022.2.5-x86_64.AppImage

![](Images/image00805.jpeg)

Click: Integrate and run

KGet

![](Images/image00806.jpeg)

Open: Software Manager

Type In or Copy and Paste:

kget

Click: Kget

![](Images/image00807.jpeg)

Click: Install

![](Images/image00808.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install kget

Press: ENTER

uGet

![](Images/image00809.jpeg)

Open: Software Manager

Type In or Copy and Paste:

uget

Click: Uget

![](Images/image00810.jpeg)

Click: Install

![](Images/image00811.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install uget

Press: ENTER

![](Images/image00812.jpeg)

Open: Snap Store

Type In or Copy and Paste:

uget

Click: uget

![](Images/image00813.jpeg)

Click: Install

![](Images/image00814.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install uget

Press: ENTER

Ebook Readers

Calibre

Fbreader

Lucidor

Calibre

![](Images/image00815.jpeg)

Open: Software Manager

Type In or Copy and Paste:

calibre

Click: Calibre

![](Images/image00816.jpeg)

Click: Install

![](Images/image00817.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install calibre

Press: ENTER

![](Images/image00818.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install imagemagick imagemagick-6-common imagemagick-6.q16 javascript-common libchm1 libjpeg-turbo-progs libjs-jquery libjs-sphinxdoc libjs-underscore libjxr-tools libjxr0 liblqr-1-0 libmagickcore-6.q16-6 libmagickcore-6.q16-6-extra libmagickwand-6.q16-6 libminizip1 libnetpbm10 libpodofo0.9.6 libqt5designer5 libqt5help5 libqt5positioning5 libqt5printsupport5 libqt5qml5 libqt5quick5 libqt5quickwidgets5 libqt5sql5 libqt5sql5-sqlite libqt5test5 libqt5webchannel5 libqt5webengine-data libqt5webengine5 libqt5webenginecore5 libqt5webenginewidgets5 libqt5xml5 libre2-5 netpbm optipng python3-apsw python3-chm python3-css-parser python3-cssselect python3-cssutils python3-dnspython python3-feedparser python3-html2text python3-html5-parser python3-html5lib python3-lxml python3-markdown python3-mechanize python3-msgpack python3-nose python3-pygments python3-pyqt5 python3-pyqt5.qtsvg python3-pyqt5.qtwebchannel python3-pyqt5.qtwebengine python3-regex python3-repoze.lru python3-routes python3-sip python3-webob python3-zeroconf

Press: ENTER

![](Images/image00819.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin

Press: ENTER

Fbreader

![](Images/image00820.jpeg)

Open: Software Manager

Type In or Copy and Paste:

fbreader

Click: Fbreader

![](Images/image00821.jpeg)

Click: Install

![](Images/image00822.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install fbreader

Press: ENTER

![](Images/image00823.jpeg)

Open: Snap Store

Type In or Copy and Paste:

fbreader

Click: FBReader 2.0

![](Images/image00824.jpeg)

Click: Install

![](Images/image00825.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install fbreader

Press: ENTER

Lucidor

![](Images/image00826.jpeg)

Go to:

[http://lucidor.org/lucidor/download.php](http://lucidor.org/lucidor/download.php)

Click: Download the deb package: lucidor_0.9.15-1_all.deb

To: Download lucidor_0.9.15-1_all.deb

Go to: Where lucidor_0.9.15-1_all.deb is downloaded

Double Click: lucidor_0.9.15-1_all.deb

![](Images/image00827.jpeg)

Click: Install Package

Elder Gaming

Dosbox

ResidualVM

ScummVM

Dosbox

![](Images/image00828.jpeg)

Open: Software Manager

Type In or Copy and Paste:

dosbox

Click: Dosbox

![](Images/image00829.jpeg)

Click: Install

![](Images/image00830.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install dosbox

Press: ENTER

![](Images/image00831.jpeg)

Open: Snap Store

Type In or Copy and Paste:

dosbox

Click: DOSBox Staging

![](Images/image00832.jpeg)

Click: Install

![](Images/image00833.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install dosbox-staging

Press: ENTER

ResidualVM

![](Images/image00834.jpeg)

Open: Software Manager

Type In or Copy and Paste:

residualvm

Click: Residualvm

![](Images/image00835.jpeg)

Click: Install

![](Images/image00836.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install residualvm

Press: ENTER

![](Images/image00837.jpeg)

Open: Snap Store

Type In or Copy and Paste:

residualvm

Click: ResidualVM

![](Images/image00838.jpeg)

Click: Install

![](Images/image00839.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install residualvm

Press: ENTER

ScummVM

![](Images/image00840.jpeg)

Open: Software Manager

Type In or Copy and Paste:

scummvm

Click: Scummvm

![](Images/image00841.jpeg)

Click: Install

![](Images/image00842.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install scummvm

Press: ENTER

![](Images/image00843.jpeg)

Open: Snap Store

Type In or Copy and Paste:

scummvm

Click: ScummVM

![](Images/image00844.jpeg)

Click: Install

![](Images/image00845.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install scummvm

Press: ENTER

File Compression and Extraction

Engrampa

p7zip-desktop

PeaZip

Engrampa

![](Images/image00846.jpeg)

Open: Software Manager

Type In or Copy and Paste:

engrampa

Click: Engrampa

![](Images/image00847.jpeg)

Click: Install

![](Images/image00848.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install engrampa

Press: ENTER

p7zip-desktop

![](Images/image00849.jpeg)

Open: Snap Store

Type In or Copy and Paste:

p7zip

Click: P7Zip - Desktop

![](Images/image00850.jpeg)

Click: Install

![](Images/image00851.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install p7zip-desktop

Press: ENTER

PeaZip

![](Images/image00852.jpeg)

Go to:

[https://peazip.github.io/peazip-linux.html](https://peazip.github.io/peazip-linux.html)

Click: DEB GTK2

To: Download peazip_8.4.0.LINUX.GTK2-1_amd64.deb

Go to: Where peazip_8.4.0.LINUX.GTK2-1_amd64.deb is downloaded

Double Click: peazip_8.4.0.LINUX.GTK2-1_amd64.deb

![](Images/image00853.jpeg)

Click: Install Package

Image Editors

Blender

GIMP or Gnu Image Manipulation Program

Krita

Pinta

Inkscape

Blender

![](Images/image00854.jpeg)

Open: Software Manager

Type In or Copy and Paste:

blender

Click: Blender

![](Images/image00855.jpeg)

Click: Install

![](Images/image00856.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install blender

Press: ENTER

![](Images/image00857.jpeg)

Open: Snap Store

Type In or Copy and Paste:

blender

Click: blender

![](Images/image00858.jpeg)

Click: Install

![](Images/image00859.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install blender

Press: ENTER

GIMP or Gnu Image Manipulation Program

![](Images/image00860.jpeg)

Open: Software Manager

Type In or Copy and Paste:

gimp

Click: Gimp

![](Images/image00861.jpeg)

Click: Install

![](Images/image00862.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install gimp

Press: ENTER

![](Images/image00863.jpeg)

Open: Snap Store

Type In or Copy and Paste:

gimp

Click: GNU Image Manipulation Program

![](Images/image00864.jpeg)

Click: Install

![](Images/image00865.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install gimp

Press: ENTER

Krita

![](Images/image00866.jpeg)

Open: Software Manager

Type In or Copy and Paste:

Krita

Click: krita

![](Images/image00867.jpeg)

Click: Install

![](Images/image00868.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install krita

Press: ENTER

![](Images/image00869.jpeg)

Open: Snap Store

Type In or Copy and Paste:

krita

Click: Krita

![](Images/image00870.jpeg)

Click: Install

![](Images/image00871.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install krita

Press: ENTER

Pinta

![](Images/image00872.jpeg)

Open: Software Manager

Type In or Copy and Paste:

pinta

Click: Pinta

![](Images/image00873.jpeg)

Click: Install

![](Images/image00874.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install pinta

Press: ENTER

![](Images/image00875.jpeg)

Open: Snap Store

Type In or Copy and Paste:

pinta

Click: Pinta

![](Images/image00876.jpeg)

Click: Install

![](Images/image00877.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install pinta

Press: ENTER

Inkscape

![](Images/image00878.jpeg)

Open: Software Manager

Type In or Copy and Paste:

inkscape

Click: Inkscape

![](Images/image00879.jpeg)

Click: Install

![](Images/image00880.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install inkscape

Press: ENTER

![](Images/image00881.jpeg)

Open: Snap Store

Type In or Copy and Paste:

inkscape

Click: Inkscape

![](Images/image00882.jpeg)

Click: Install

![](Images/image00883.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install inkscape

Press: ENTER

Internet Video Broadcasting

*   OBS Studio

OBS Studio

![](Images/image00884.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install ffmpeg

Press: ENTER

![](Images/image00885.jpeg)

Open: Snap Store

Type In or Copy and Paste:

obs studio

Click: OBS Studio

![](Images/image00886.jpeg)

Click: Install

![](Images/image00884.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install ffmpeg

Press: ENTER

![](Images/image00887.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install obs-studio

Press: ENTER

![](Images/image00884.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install ffmpeg

Press: ENTER

![](Images/image00888.jpeg)

Open: Software Manager

Type In or Copy and Paste:

obs studio

Click: Obs-studio

![](Images/image00889.jpeg)

Click: Install

![](Images/image00884.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install ffmpeg

Press: ENTER

![](Images/image00890.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install obs-studio

Press: ENTER

Media Player

*   Parole
*   SMPlayer
*   VLC

Parole

![](Images/image00891.jpeg)

Open: Software Manager

Type In or Copy and Paste:

parole

Click: Parole

![](Images/image00892.jpeg)

Click: Install

![](Images/image00893.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install parole

Press: ENTER

SMPlayer

![](Images/image00894.jpeg)

Open: Software Manager

Type In or Copy and Paste:

smplayer

Click: Smplayer

![](Images/image00895.jpeg)

Click: Install

![](Images/image00896.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install smplayer

Press: ENTER

VLC

![](Images/image00897.jpeg)

Open: Software Manager

Type In or Copy and Paste:

vlc

Click: VLC

![](Images/image00898.jpeg)

Click: Install

![](Images/image00899.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install vlc

Press: ENTER

![](Images/image00900.jpeg)

Open: Snap Store

Type In or Copy and Paste:

vlc

Click: VLC

![](Images/image00901.jpeg)

Click: Install

![](Images/image00902.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install vlc

Press: ENTER

Modern Gaming

*   Blizzard Battle.net
*   Lutris
*   Proton-QT
*   Steam
*   WINE

Blizzard Battle.net

![](Images/image00903.jpeg)

Open: Lutris

Click: Community Installers

Click: Search Bar

Type In or Copy and Paste:

blizzard battle.net

Select: Blizzard Battle.net

Click: Install

![](Images/image00904.jpeg)

Click: Install

![](Images/image00905.jpeg)

Click: Install

![](Images/image00906.jpeg)

Wait for file to download

![](Images/image00907.jpeg)

Click: Continue

![](Images/image00908.jpeg)

Click: Install

![](Images/image00909.jpeg)

Click: Create desktop shortcut

Click: Create application menu shortcut

Click: Close

Lutris

![](Images/image00910.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo add-apt-repository ppa:lutris-team/lutris

Press: ENTER

![](Images/image00784.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image00911.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install lutris

Press: ENTER

Proton-QT

![](Images/image00912.jpeg)

Go to:

[https://github.com/DavidoTek/ProtonUp-Qt/releases/tag/v2.5.0](https://github.com/DavidoTek/ProtonUp-Qt/releases/tag/v2.5.0)

Click: ProtonUp-Qt-2.5.0-x86_64.AppImage

To: Download ProtonUp-Qt-2.5.0-x86_64.AppImage

Go to: Where ProtonUp-Qt-2.5.0-x86_64.AppImage is downloaded

Double Click: ProtonUp-Qt-2.5.0-x86_64.AppImage

![](Images/image00913.jpeg)

Click: Integrate and run

Steam

![](Images/image00914.jpeg)

Open: Software Manager

Type In or Copy and Paste:

steam

Click: Steam

![](Images/image00915.jpeg)

Click: Install

![](Images/image00916.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install steam

Press: ENTER

WINE

![](Images/image00780.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo dpkg --add-architecture i386

Press: ENTER

![](Images/image00781.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image00782.jpeg)

Open: Terminal

Type In or Copy and Paste:

wget -qO- https://dl.winehq.org/wine-builds/winehq.key | sudo apt-key add -

Press: ENTER

![](Images/image00783.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt-add-repository 'deb http://dl.winehq.org/wine-builds/ubuntu/ bionic main'

Press: ENTER

![](Images/image00784.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image00785.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt-get install --install-recommends winehq-staging

Press: ENTER

Music On Demand Streaming

*   Amazon Music Unlimited
*   Apple Music
*   Spotify Client
*   Spotify
*   Tidal
*   Youtube Music

Amazon Music

![](Images/image00917.jpeg)

Go to:

[https://www.amazon.co.uk/music/unlimited](https://www.amazon.co.uk/music/unlimited)

Sign in to Access

Apple Music

![](Images/image00918.jpeg)

Go to:

[https://music.apple.com/gb/browse](https://music.apple.com/gb/browse)

Sign in to Access

Spotify

![](Images/image00919.jpeg)

Go to:

[https://open.spotify.com/](https://open.spotify.com/)

Sign in to Access

Spotify Client

![](Images/image00920.jpeg)

Open: Snap Store

Type In or Copy and Paste:

spotify

Click: spotify

![](Images/image00921.jpeg)

Click: Install

Tidal Access Using Website

![](Images/image00922.jpeg)

Go to:

[https://tidal.com/](https://tidal.com/)

Sign in to Access

Youtube Music

![](Images/image00923.jpeg)

Go to:

[https://music.youtube.com/](https://music.youtube.com/)

Sign in to Access

*   Music Players

*   Audacious
*   Clementine
*   DeaDBeeF

◦ Audacious

![](Images/image00924.jpeg)

Open: Software Manager

Type In or Copy and Paste:

audacious

Click: Audacious

![](Images/image00925.jpeg)

Click: Install

![](Images/image00926.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install audacious

Press: ENTER

◦ Clementine

![](Images/image00927.jpeg)

Open: Software Manager

Type In or Copy and Paste:

clementine

Click: Clementine

![](Images/image00928.jpeg)

Click: Install

![](Images/image00929.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install clementine

Press: ENTER

![](Images/image00930.jpeg)

Open: Snap Store

Type In or Copy and Paste:

clementine

Click: clementine

![](Images/image00931.jpeg)

Click: Install

![](Images/image00932.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install clementine

Press: ENTER

DeaDBeeF

![](Images/image00933.jpeg)

Open: Snap Store

Type In or Copy and Paste:

deadbeef

Click: deadbeef-vs

![](Images/image00934.jpeg)

Click: Install

![](Images/image00935.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install deadbeef-vs

Press: ENTER

Office Suites

LibreOffice

ONLYOFFICE Desktop Editors

OpenOffice

SoftMaker FreeOffice

WPS Office

LibreOffice

![](Images/image00936.jpeg)

Open: Snap Store

Type In or Copy and Paste:

libreoffice

Click: libreoffice

![](Images/image00937.jpeg)

Click: Install

![](Images/image00938.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install libreoffice

Press: ENTER

![](Images/image00939.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo add-apt-repository ppa:libreoffice/ppa

Press: ENTER

![](Images/image00940.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image00941.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt upgrade

Press: ENTER

ONLYOFFICE Desktop Editors

![](Images/image00942.jpeg)

Open: Snap Store

Type In or Copy and Paste:

onlyoffice

Click: ONLYOFFICE Desktop Editors

![](Images/image00943.jpeg)

Click: Install

![](Images/image00944.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install onlyoffice-desktopeditors

Press: ENTER

![](Images/image00945.jpeg)

Go to:

[https://www.onlyoffice.com/en/download-desktop.aspx?from=desktop](https://www.onlyoffice.com/en/download-desktop.aspx?from=desktop)

Click: DOWNLOAD DEB under Debian 8, Ubuntu 14.04 and higher

To: Download onlyoffice-desktopeditors_amd64.deb

Go to: Where onlyoffice-desktopeditors_amd64.deb is downloaded

Double Click: onlyoffice-desktopeditors_amd64.deb

![](Images/image00946.jpeg)

Click: Install Package

OpenOffice

![](Images/image00947.jpeg)

Go to:

[https://apprepo.de/appimage/openoffice](https://apprepo.de/appimage/openoffice)

Click:  DOWNLOAD

To: Download OpenOffice.AppImage

Go to: Where OpenOffice.AppImage is downloaded

Double Click: OpenOffice.AppImage

![](Images/image00948.jpeg)

Click: Integrate and run

SoftMaker FreeOffice

![](Images/image00949.jpeg)

Go to:

[https://www.freeoffice.com/en/download/applications](https://www.freeoffice.com/en/download/applications)

Click: Download Under Linux

Click: .deb package for DEB-based systems

To: Download softmaker-freeoffice-2021_1042-01_amd64.deb

Go to: Where softmaker-freeoffice-2021_1042-01_amd64.deb is downloaded

Double Click: softmaker-freeoffice-2021_1042-01_amd64.deb

![](Images/image00950.jpeg)

Click: Install Package

WPS Office

![](Images/image00951.jpeg)

Go to:

[https://www.wps.com/](https://www.wps.com/)

Click: Free Download

Click: Deb Package

To: Download wps-office_11.1.0.10920.XA_amd64.deb

Go to: Where wps-office_11.1.0.10920.XA_amd64.deb is downloaded

Double Click: wps-office_11.1.0.10920.XA_amd64.deb

![](Images/image00952.jpeg)

Click: Install Package

PDF Readers

Evince

*   Okular

Evince

![](Images/image00953.jpeg)

Open: Software Manager

Type In or Copy and Paste:

evince

Click: Evince

![](Images/image00954.jpeg)

Click: Install

![](Images/image00955.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install evince

Press: ENTER

![](Images/image00956.jpeg)

Open: Snap Store

Type In or Copy and Paste:

evince

Click: Evince

![](Images/image00957.jpeg)

Click: Install

![](Images/image00958.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install evince

Press: ENTER

Okular

![](Images/image00959.jpeg)

Open: Software Manager

Type In or Copy and Paste:

okular

Click: Okular

![](Images/image00960.jpeg)

Click: Install

![](Images/image00961.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install okular

Press: ENTER

![](Images/image00962.jpeg)

Open: Snap Store

Type In or Copy and Paste:

okular

Click: Okular

![](Images/image00963.jpeg)

Click: Install

![](Images/image00964.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install okular

Press: ENTER

Remote Working

Citrix Workspace

Microsoft Teams

Zoom

Citrix Workspace

![](Images/image00965.jpeg)

Go to:

[https://www.citrix.com/en-gb/downloads/workspace-app/linux/workspace-app-for-linux-latest.html](https://www.citrix.com/en-gb/downloads/workspace-app/linux/workspace-app-for-linux-latest.html)

Click: Download File under Citrix Workspace app for Linux (x86_64)

To: Download icaclient_22.2.0.20_amd64.deb

Go to: Where icaclient_22.2.0.20_amd64.deb is downloaded

Double Click: icaclient_22.2.0.20_amd64.deb

![](Images/image00966.jpeg)

Click: Install Package

Microsoft Teams

![](Images/image00967.jpeg)

Open: Snap Store

Type In or Copy and Paste:

microsoft teams

Click: Microsoft Teams (Insiders or Preview)

![](Images/image00968.jpeg)

Click: Install

Zoom

![](Images/image00784.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image00969.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install libglib2.0-0 libxcb-shape0 libxcb-shm0 libxcb-xfixes0 libxcb-randr0 libxcb-image0 libfontconfig1 libgl1-mesa-glx libxi6 libsm6 libxrender1 libpulse0 libxcomposite1 libxslt1.1 libsqlite3-0 libxcb-keysyms1 libxcb-xtest0 ibus

Press: ENTER

![](Images/image00970.jpeg)

Go to:

[https://zoom.us/download?os=linux](https://zoom.us/download?os=linux)

Click: Box in same row as Linux Type

Click: Mint

Click: Box in same row as OS Architecture

Click: 64 bit

Click: Box in same row as Version

Click: 18+

To: Download zoom_amd64.deb

Go to: Where zoom_amd64.deb is downloaded

Double Click: zoom_amd64.deb

![](Images/image00971.jpeg)

Click: Install Package

Security

*   All The Firewall Ports I Use

◦ TCP Ports With Spaces

◦ TCP Ports Without Spaces

◦ UDP Ports With Spaces

◦ UDP Ports Without Spaces

*   Bitwarden
*   Buttercup
*   ClamAV
*   ClamAV Realtime
*   ClamTK
*   ClamTK Right Click To Scan
*   Firetools
*   Firejail
*   GUFW

◦ GUFW Set Multi Port Rules

◦ GUFW Set Range Port Rules

◦ GUFW Set Single Port Rules

*   UFW

◦ UFW Set Multi and Range Port Rules

◦ UFW Set Multi Port Rules

◦ UFW Set Range Port Rules

◦ UFW Set Single Port Rules

◦ All Of The Firewall Ports I Use

These are all of the firewall rules that I are utilized on a daily basis with all of the games

and software that I use.

▪ TCP Ports With Spaces

53, 80 ,433, 443, 1119 ,1120 , 2099, 3074, 3075, 3216, 3478, 3479, 3569, 3724, 4000,

5060, 5062, 5222, 5223, 6012, 6112, 6113, 6114, 6250, 8080, 8088, 8094, 8097, 9946,

9988, 14000, 14008, 14020, 14021, 14022, 14023, 14024, 17502, 17503, 17504, 18000,

18060, 18120, 22990, 27900, 28910, 29900, 42124, 42125, 42126, 42127, 42130, 42210,

42230, 10000:19999, 10000:20000, 10000:29999, 1024:1124, 1119:1120, 12000:65000,

20000:20100, 25000:25099, 27014:27050, 30000:30099, 42100:42200, 6112:6119,

6113:6119, 7777:7780, 8393:8400, 9960:9969

▪ TCP Ports Without Spaces

53,80,433,443,1119,1120,2099,3074,3075,3216,3478,3479,3569,3724,4000,5060,5062,5222,5223,6012,6112,6113,6114,6250,8080,8088,8094,8097,9946,9988,14000,14008,14020,14021,14022,14023,14024,17502,17503,17504,18000,18060,18120,22990,27900,28910,29900,42124,42125,42126,42127,42130,42210,42230,10000:19999,10000:20000,10000:29999,1024:1124,1119:1120,12000:65000,20000:20100,25000:25099,27014:27050,30000:30099,42100:42200,6112:6119,6113:6119,7777:7780,8393:8400,9960:9969

▪ UDP Ports With Spaces

67 ,80 ,443 ,1119 ,1120 ,3074 ,3126 ,3478 ,3659 ,3724 ,4000 ,5060 ,5062 ,6012 ,6112 ,61

13 ,6114 ,6120, 6250, 8080, 8088, 8125, 9565, 9570, 18000, 27036, 29900, 30000:30099,

9000:9999, 10000:19999, 1024:1124, 1119:1120, 12000:64000, 14000:14016,

21000:26000, 22990:23006, 25000:25099, 25200:25300, 27000:27031, 3074:3083,

3478:3479, 37000:39999, 37000:40000, 4379:4380, 5000:5500, 6112:6119

▪ UDP Ports Without Spaces

67,80,443,1119,1120,3074,3126,3478,3659,3724,4000,5060,5062,6012,6112,61

13,6114,6120,6250,8080,8088,8125,9565,9570,18000,27036,29900,30000:300

99,9000:9999,10000:19999,1024:1124,1119:1120,12000:64000,14000:14016,21

000:26000,22990:23006,25000:25099,25200:25300,27000:27031,3074:3083,34

78:3479,37000:39999,37000:40000,4379:4380,5000:5500,6112:6119

Bitwarden

![](Images/image00972.jpeg)

Open: Snap Store

Type In or Copy and Paste:

bitwarden

Click: bitwarden

![](Images/image00973.jpeg)

Click: Install

![](Images/image00974.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install bitwarden

Press: ENTER

Buttercup

![](Images/image00975.jpeg)

Go to:

[https://github.com/buttercup/buttercup-desktop/releases/tag/v2.14.2](https://github.com/buttercup/buttercup-desktop/releases/tag/v2.14.2)

Click: Buttercup-linux-x86_64.AppImage

To: Download Buttercup-linux-x86_64.AppImage

Go to: Where Buttercup-linux-x86_64.AppImage is downloaded

Double Click: Buttercup-linux-x86_64.AppImage

![](Images/image00976.jpeg)

Click: Integrate and run

ClamAV

![](Images/image00977.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install clamav

Press: ENTER

ClamAV Realtime

![](Images/image00978.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt-get install clamav-daemon

Press: ENTER

![](Images/image00979.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo systemctl enable clamav-daemon

Press: ENTER

![](Images/image00980.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo systemctl start clamav-daemon

Press: ENTER

ClamTK

![](Images/image00981.jpeg)

Open: Software Manager

Type In or Copy and Paste:

clamtk

Click: Clamtk

![](Images/image00982.jpeg)

Click: Install

![](Images/image00983.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install clamtk

Press: ENTER

ClamTK Right Click To Scan

![](Images/image00984.jpeg)

Open: Software Manager

Type In or Copy and Paste:

clamtk gnome

Click: Clamtk-gnome

![](Images/image00985.jpeg)

Click: Install

![](Images/image00986.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install clamtk-gnome

Press: ENTER

Firetools

![](Images/image00987.jpeg)

Open: Software Manager

Type In or Copy and Paste:

firetools

Click: Firetools

![](Images/image00988.jpeg)

Click: Install

![](Images/image00989.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install firetools

Press: ENTER

Firejail

![](Images/image00990.jpeg)

Open: Software Manager

Type In or Copy and Paste:

firejail

Click: Firejail

![](Images/image00991.jpeg)

Click: Install

![](Images/image00992.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install firejail

Press: ENTER

GUFW

![](Images/image00993.jpeg)

Open: Software Manager

Type In or Copy and Paste:

gufw

Click: Gufw

![](Images/image00994.jpeg)

Click: Install

![](Images/image00995.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install gufw

Press: ENTER

GUFW Set Multi Port Rules

![](Images/image00996.jpeg)

Open: Gufw or Firewall Configuration

Click: Rules

Click: +

Click: Simple

Choose: TCP or UDP

Type In or Copy and Paste:

21,22

Click: Add

GUFW Set Range Port Rules

![](Images/image00997.jpeg)

Open: Gufw or Firewall Configuration

Click: Rules

Click: +

Click: Simple

Choose: TCP or UDP

Type In or Copy and Paste:

4001:4002

Click: Add

GUFW Set Single Port Rules

![](Images/image00998.jpeg)

Open: Gufw or Firewall Configuration

Click: Rules

Click: +

Click: Simple

Choose: TCP or UDP

Type In or Copy and Paste:

21

Click: Add

UFW

![](Images/image00999.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install ufw

Press: ENTER

UFW Set Multi and Range Port Rules

![](Images/image01000.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo ufw allow 21,22,4111:4112/tcp

Press: ENTER

Change /tcp to /udp for UDP Protocol

UFW Set Multi Port Rules

![](Images/image01001.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo ufw allow 21,22/tcp

Press: ENTER

Change /tcp to /udp for UDP Protocol

UFW Set Range Port Rules

![](Images/image01002.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo ufw allow 4111:4112/tcp

Press: ENTER

Change /tcp to /udp for UDP Protocol

UFW Set Single Port Rules

![](Images/image01003.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo ufw allow 21/tcp

Press: ENTER

Change /tcp to /udp for UDP Protocol

Software Distribution

AppImageLauncher

Flathub

Flatpak

Java JRE JDK

Snap

Snap Store

AppImageLauncher

![](Images/image01004.jpeg)

Go to:

[https://github.com/TheAssassin/AppImageLauncher/releases/tag/v2.2.0](https://github.com/TheAssassin/AppImageLauncher/releases/tag/v2.2.0)

Click:  appimagelauncher_2.2.0-travis995.0f91801.bionic_amd64.deb 

To: Download appimagelauncher_2.2.0-travis995.0f91801.bionic_amd64.deb

![](Images/image01005.jpeg)

Go to: Where appimagelauncher_2.2.0-travis995.0f91801.bionic_amd64.deb  is downloaded

Double Click: appimagelauncher_2.2.0-travis995.0f91801.bionic_amd64.deb

Click: Install Package

![](Images/image01006.jpeg)

Click: Continue

Flathub

![](Images/image01007.jpeg)

Open: Terminal

Type In or Copy and Paste:

flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo              

Press: ENTER

Flatpak

![](Images/image00784.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image01008.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install flatpak

Press: ENTER

Java JRE JDK

![](Images/image01009.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install default-jdk default-jre

Press: ENTER

Snap

![](Images/image01010.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo mv /etc/apt/preferences.d/nosnap.pref ~/Documents/nosnap.backup

Press: ENTER

![](Images/image00784.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image01011.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install snapd

Press: ENTER

Snap Store

![](Images/image01012.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install snap-store

Press: ENTER

System Settings

*   Alt-Tab Thumbnails
*   AMD Drivers
*   Auto Mount Disks
*   Changing Kernel Versions
*   Changing Mouse Acceleration
*   Changing Sound Device
*   Changing Themes
*   Enable LibreOffice Night Mode
*   How To Block Websites Using Xed
*   libopusfile0
*   Nautilus File Manager
*   Night Light
*   Nvidia Drivers
*   Possible Intel Sound Crackle Fix
*   Possible Parole Segmentation Fault Fix
*   Set As Default For File Type
*   Setting Alternative DNS
*   Startup Applications
*   Updating System

Alt-Tab Thumbnails

![](Images/image01013.jpeg)

Open: Windows

Click: Alt-Tab

Click: Box in same row as Alt-Tab switcher style

Click: Thumbnails only

AMD Drivers

![](Images/image01014.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo add-apt-repository ppa:kisak/kisak-mesa

Press: ENTER

![](Images/image01015.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image01016.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt-get upgrade

Press: ENTER

![](Images/image01017.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt-get install mesa

Press: ENTER

![](Images/image01018.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt-get install ppa-purge

Press: ENTER

![](Images/image01019.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo ppa-purge ppa:kisak/kisak-mesa

Press: ENTER

![](Images/image00784.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image00941.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt upgrade

Press: ENTER

Auto Mount Disks

![](Images/image01020.jpeg)

Open: Disks

Select: Disk

Select: Volume

Click: Cog icon

Click: Edit Mount Options

![](Images/image01021.jpeg)

Move: Switch in same row as User Session Defaults, to the left

Click: OK

![](Images/image01022.jpeg)

Click: Play button

Changing Kernel Versions

![](Images/image01023.jpeg)

Open: Update Manager

Click: View

Click: Linux Kernels

![](Images/image01024.jpeg)

Can choose to Continue or not to continue

![](Images/image01025.jpeg)

Click: 5.13

Click: Install

![](Images/image01026.jpeg)

Click: Yes

Changing Mouse Acceleration

![](Images/image01027.jpeg)

Open: Mouse and Touchpad

Move: Switch in same row as Custom Acceleration to the right

Move: Switch under Acceleration all the way to Fast

Changing Sound Device

![](Images/image01028.jpeg)

Open: Sound

Click: Device to Switch to that Sound Device

Changing Themes

![](Images/image01029.jpeg)

Open: Themes

Click: Box in same row as Controls

Click: Mint-Y-Dark

Click: Box in same row as Desktop

Click: Mint-Y-Dark

Enable LibreOffice Night Mode

![](Images/image01030.jpeg)

Open: LibreOffice

Click: Tools

Click: Options

Click: Application Colours

Click: Box in same row as Document background

Click: Dark Grey 1

Click: Box in same row as Application background

Click: Dark Grey 2

Click: Apply

How To Block Websites Using Xed

![](Images/image01031.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo xed /etc/hosts

![](Images/image01032.jpeg)

Go to: End of File

Type In or Copy and Paste:

127.0.0.1 www.example.com example.com

Press: CTRL + S

Click: File

Click: Save

libopusfile0

![](Images/image01033.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install libopusfile0

Press: ENTER

Nautilus File Manager

![](Images/image01034.jpeg)

Open: Software Manager

Type In or Copy and Paste:

nautilus

Click: Nautilus

![](Images/image01035.jpeg)

Click: Install

![](Images/image01036.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install nautilus

Press: ENTER

Night Light

![](Images/image01037.jpeg)

Open: Redshift

Click: Redshift icon in system tray on the bottom right

Make: Sure the boxes in the same rows as Enable and Autostart are ticked

Nvidia Drivers

![](Images/image01038.jpeg)

Open: Driver Manager

Select: nvidia-driver-510

Click: Apply Changes

![](Images/image01039.jpeg)

Wait as changes are Applied

![](Images/image01040.jpeg)

Click: Restart

Possible Intel Sound Crackle Fix

![](Images/image01041.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo echo "options snd_hda_intel power_save=0" | sudo tee -a /etc/modprobe.d/audio_disable_powersave.conf

Press: ENTER

Possible Parole Segmentation Fault Fix

![](Images/image01042.jpeg)

Open: Files

Go to:

/home/mylinuxmintpc/.config/xfce4

Select: parole

Right Click: parole

Click: Delete

Set As Default For File Type

![](Images/image01043.jpeg)

Right Click: File

Click: Properties

Click: Open With

Click: Application

Click: Set as default

Click: Close

Setting Alternative DNS

![](Images/image01044.jpeg)

Go to:

[https://www.quad9.net/](https://www.quad9.net/)

Take Note: Of the IPv4 and IPv6 Addresses

Open: Network

![](Images/image01045.jpeg)

Select: Connection

Click: Cog icon

![](Images/image01046.jpeg)

Click: IPv4

Move: Switch in same row as: Automatic and DNS to the left

Click: + Button under DNS

Click: First box next to Server

Type In or Copy and Paste:

9.9.9.9

Click: Second box next to Server

Type In or Copy and Paste:

149.112.112.112

Click: IPv6

![](Images/image01047.jpeg)

Click: IPv6

Move: Switch in same row as: Automatic and DNS to the left

Click: + Button under DNS

Click: First box next to Server

Type In or Copy and Paste:

2620:fe::fe

Click: Second box next to Server

Type In or Copy and Paste:

2620:fe::9

Click: Apply

Other Alternative DNS Available are:

*   Comodo Secure DNS

◦ [https://www.comodo.com/secure-dns/switch/](https://www.comodo.com/secure-dns/switch/)

◦ IPv4

▪ 8.26.56.26

▪ 8.20.247.20

*   DNS.WATCH

◦ [https://dns.watch/](https://dns.watch/)

◦ IPv4

▪ 84.200.69.80

▪ 84.200.69.80

◦ IPv6

▪ 2001:1608:10:25::1c04:b12f

▪ 2001:1608:10:25::9249:d69b

*   OpenNIC Project

◦ [https://www.opennic.org/](https://www.opennic.org/)

◦ IPv4

▪ 94.247.43.254

▪ 194.36.144.87

▪ 151.80.222.79

▪ 91.217.137.37

◦ IPv6

▪  

▪ 2a00:f826:8:1::254

▪ 2a03:4000:4d:c92:88c0:96ff:fec6:b9d

▪ 2001:470:1f15:b80::53

▪ 2001:67c:13e4:1::37

Startup Applications

![](Images/image01048.jpeg)

Open: Startup Applications

Click: +

Click: Choose Application

![](Images/image01049.jpeg)

Click: Firefox Web Browser

Click: Add Application

![](Images/image01050.jpeg)

Open: Startup Applications

Click: +

Click: Custom Command

![](Images/image01051.jpeg)

Click: Box in the same row as Name

Type In or Copy and Paste:

Firefox

Click: Box in the same row as Command

Type In or Copy and Paste:

firefox

Click: Add

Updating System

![](Images/image01052.jpeg)

Open: Update Manager

Choose: Not to download from Local Mirror

Choose: To Update the Update Manager

Click: Refresh

Click: Install Updates

![](Images/image01053.jpeg)

Click: OK

![](Images/image01054.jpeg)

Wait for Changes to be Applied

![](Images/image01055.jpeg)

Backup and Save your Progress and Files

![](Images/image01056.jpeg)

Press: Super or Meta key

Click: Power Icon (Facing up)

![](Images/image01057.jpeg)

Click: Restart

System Utilities

Bleachbit

Boot Repair

Czkawka

GParted

gpustat

Grub Customizer

HardInfo

K4DirStat

KDE Partition Manager

Neofetch

Psensor

QDirStat

Stacer

Sweeper

Bleachbit

![](Images/image01058.jpeg)

Open: Software Manager

Type In or Copy and Paste:

bleachbit

Click: Bleachbit

![](Images/image01059.jpeg)

Click: Install

![](Images/image01060.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install bleachbit

Press: ENTER

Boot Repair

![](Images/image01061.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo add-apt-repository ppa:yannubuntu/boot-repair && sudo apt update

Press: ENTER

![](Images/image01062.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install -y boot-repair && boot-repair

Press: ENTER

Czkawka

![](Images/image01063.jpeg)

Open: Snap Store

Type In or Copy and Paste:

czkawka

Click: Czkawka

![](Images/image01064.jpeg)

Click: Install

![](Images/image01065.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install czkawka

Press: ENTER

GParted

![](Images/image01066.jpeg)

Open: Software Manager

Type In or Copy and Paste:

gparted

Click: Gparted

![](Images/image01067.jpeg)

Click: Install

![](Images/image01068.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install gparted

Press: ENTER

gpustat

![](Images/image01069.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install gpustat

Press: ENTER

Grub Customizer

![](Images/image01070.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image01071.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install grub-customizer

Press: ENTER

HardInfo

![](Images/image01072.jpeg)

Open: Software Manager

Type In or Copy and Paste:

hardinfo

Click: Hardinfo

![](Images/image01073.jpeg)

Click: Install

![](Images/image01074.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install hardinfo

Press: ENTER

K4DirStat

![](Images/image01075.jpeg)

Open: Software Manager

Type In or Copy and Paste:

k4dirstat

Click: K4dirstat

![](Images/image01076.jpeg)

Click: Install

![](Images/image01077.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install k4dirstat

Press: ENTER

KDE Partition Manager

![](Images/image01078.jpeg)

Open: Software Manager

Type In or Copy and Paste:

partitionmanager

Click: Partitionmanager

![](Images/image01079.jpeg)

Click: Install

![](Images/image01080.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install partitionmanager

Press: ENTER

Neofetch

![](Images/image01081.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install neofetch

Press: ENTER

![](Images/image01082.jpeg)

Open: Terminal

Type In or Copy and Paste:

neofetch

Press: ENTER

Psensor

![](Images/image01083.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install lm-sensors

Press: ENTER

![](Images/image01084.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo sensors-detect

Press: ENTER

![](Images/image01085.jpeg)

Open: Terminal

Type In or Copy and Paste:

sensors

Press: ENTER

![](Images/image01086.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install psensors

Press: ENTER

QDirStat

![](Images/image01087.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install qdirstat

Press: ENTER

Stacer

![](Images/image01088.jpeg)

Open: Software Manager

Type In or Copy and Paste:

stacer

Click: Stacer

![](Images/image01089.jpeg)

Click: Install

![](Images/image01090.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install stacer

Press: ENTER

Sweeper

![](Images/image01091.jpeg)

Open: Software Manager

Type In or Copy and Paste:

sweeper

Click: Sweeper

![](Images/image01092.jpeg)

Click: Install

![](Images/image01093.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install sweeper

Press: ENTER

![](Images/image01094.jpeg)

Open: Snap Store

Type In or Copy and Paste:

sweeper

Click: sweeper

![](Images/image01095.jpeg)

Click: Install

![](Images/image01096.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install sweeper

Press: ENTER

Video Editors

Kdenlive

Openshot

Shotcut

Kdenlive

![](Images/image01097.jpeg)

Open: Software Manager

Type In or Copy and Paste:

kdenlive

Click: Kdenlive

![](Images/image01098.jpeg)

Click: Install

![](Images/image01099.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install kdenlive

Press: ENTER

![](Images/image01100.jpeg)

Open: Snap Store

Type In or Copy and Paste:

kdenlive

Click: kdenlive

![](Images/image01101.jpeg)

Click: Install

![](Images/image01102.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install kdenlive

Press: ENTER

Openshot

![](Images/image01103.jpeg)

Open: Software Manager

Type In or Copy and Paste:

openshot

Click: OpenShot Video Editor

![](Images/image01104.jpeg)

Click: Install

![](Images/image01105.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install openshot

Press: ENTER

Shotcut

![](Images/image01106.jpeg)

Open: Software Manager

Type In or Copy and Paste:

shotcut

Click: Shotcut

![](Images/image01107.jpeg)

Click: Install

![](Images/image01108.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install shotcut

Press: ENTER

![](Images/image01109.jpeg)

Open: Snap Store

Type In or Copy and Paste:

shotcut

Click: shotcut

![](Images/image01110.jpeg)

Click: Install

![](Images/image01111.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install shotcut

Press: ENTER

Video On Demand Streaming

*   Amazon Prime Video
*   Disney+
*   Netflix

Amazon Prime Video

![](Images/image01112.jpeg)

Go to:

[https://www.amazon.co.uk/Amazon-Video/b?node=3010085031](https://www.amazon.co.uk/Amazon-Video/b?node=3010085031)

Sign in to Access

Disney+

![](Images/image01113.jpeg)

Go to:

[https://www.disneyplus.com/en-gb](https://www.disneyplus.com/en-gb) 

Sign in to Access

Netflix

![](Images/image01114.jpeg)

Go to:

[https://www.netflix.com/gb/](https://www.netflix.com/gb/)

Sign in to Access

Virtualization

Virt-Manager

Virtualbox

Virtualbox Extension Pack

Virt-Manager

![](Images/image01115.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virtinst virt-manager

Press: ENTER

Virtualbox

![](Images/image01116.jpeg)

Open: Software Manager

Type In or Copy and Paste:

virtualbox

Click: Virtualbox

![](Images/image01117.jpeg)

Click: Install

![](Images/image00784.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt update

Press: ENTER

![](Images/image01118.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install virtualbox

Press: ENTER

Virtualbox Extension Pack

![](Images/image01119.jpeg)

Open: Software Manager

Type In or Copy and Paste:

virtualbox

Click: Virtualbox-ext-pack

![](Images/image01120.jpeg)

Click: Install

![](Images/image01121.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo apt install virtualbox-ext-pack

Press: ENTER

Web Browsers

Chromium

Firefox ESR

Google Chrome

Microsoft Edge

Opera

Chromium

![](Images/image01122.jpeg)

Open: Snap Store

Type In or Copy and Paste:

chromium

Click: chromium

![](Images/image01123.jpeg)

Click: Install

![](Images/image01124.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install chromium

Press: ENTER

Firefox ESR

![](Images/image01125.jpeg)

Go to:

[https://www.mozilla.org/en-GB/firefox/all/#product-desktop-esr](https://www.mozilla.org/en-GB/firefox/all/#product-desktop-esr)

Click: Box under Which browser would you like to download?

Click: Firefox Extended Support Release

Click: Box under Select your preferred installer

Click: Linux 64-bit

Click: Box under Select your preferred language

Click: English (British)

To: Download firefox-91.6.0esr.tar.bz2

Go to: Where firefox-91.6.0esr.tar.bz2 is downloaded

Double Click: firefox-91.6.0esr.tar.bz2

![](Images/image01126.jpeg)

Select: firefox

Click: Extract

![](Images/image01127.jpeg)

Go to:

/home/mylinuxmintpc/Applications

Click: Extract

Click: Close

Google Chrome

![](Images/image01128.jpeg)

Go to:

[https://www.google.com/intl/en_uk/chrome/](https://www.google.com/intl/en_uk/chrome/)

Click: Download Chrome

Tick: Box in same row as 64 bit.deb (For Debian/Ubuntu)

Click: Accept and install

To: Download google-chrome-stable_current_amd64.deb

Go to: Where google-chrome-stable_current_amd64.deb is downloaded

Double Click: google-chrome-stable_current_amd64.deb

![](Images/image01129.jpeg)

Click: Install Package

Microsoft Edge

![](Images/image01130.jpeg)

Go to:

[https://www.microsoftedgeinsider.com/en-us/](https://www.microsoftedgeinsider.com/en-us/)

Click: for Linux (deb) Debian/Ubuntu

![](Images/image01131.jpeg)

If choose to accept

Click: Accept and download

![](Images/image01132.jpeg)

Click: Install Package

Opera

![](Images/image01133.jpeg)

Open: Snap Store

Type In or Copy and Paste:

opera

Click: Opera

![](Images/image01134.jpeg)

Click: Install

![](Images/image01135.jpeg)

Open: Terminal

Type In or Copy and Paste:

sudo snap install opera

Press: ENTER

World of Warcraft

Battle.net Launch Arguments

In-Game Store Lutris Black Screen Fix

In-Game Store WINE Black Screen Fix

Lutris Battle.net Runner and System Options

Manually Installing World of Warcraft Addons

Battle.net Launch Arguments

![](Images/image01136.jpeg)

Open: Battle.net

Click: The World of Warcraft Icon

Click: The cog icon next to the Play icon

Click: Game Settings

Tick: Box in the same row as Additional command line arguments

Click: Box below Additional command line arguments

Type In or Copy and Paste:

-d3d11

Repeat for World of Warcraft Classic and TBC Classic

Click: Done

In-Game Store Lutris Black Screen Fix

![](Images/image01137.jpeg)

Open: Lutris

Click: Games

Select: Blizzard Battle.net

Click: Up Arrow next to the WINE glass symbol

Click: Wine configuration

![](Images/image01138.jpeg)

Click: Drives

Click: Add

![](Images/image01139.jpeg)

Select Drive Letter from Drop Down Box

Click: OK

I usually just click OK straight away

![](Images/image01140.jpeg)

Select: Newly created Drive Letter

Click: Browse

![](Images/image01141.jpeg)

Select: mnt

Expand: mnt folder by clicking on the + symbol

Expand: folder of drive where World of Warcraft is located

![](Images/image01142.jpeg)

Go to: Where the World of Warcraft folder is located and installed

Select: World of Warcraft

Click: OK

In-Game Store WINE Black Screen Fix

![](Images/image01143.jpeg)

Open: Terminal

Type In or Copy and Paste:

winecfg

Press: Enter

![](Images/image01144.jpeg)

Select: Drop down box next to Windows Version

Click: Windows 10

Click: Apply

Click: Staging

![](Images/image01145.jpeg)

Tick Boxes in the same row as:

*   Enable CSMT for better graphical performance (deprecated)
*   Enable VAAPI as backend for DXVA2 GPU decoding

Click: Drives

![](Images/image01138.jpeg)

Click: Add

![](Images/image01139.jpeg)

Select Drive Letter from Drop Down Box

Click: OK

I usually just click OK straight away

![](Images/image01140.jpeg)

Select: Newly created Drive Letter

Click: Browse

![](Images/image01141.jpeg)

Select: mnt

Expand: mnt folder by clicking on the + symbol

Expand: folder of drive where World of Warcraft is located

![](Images/image01142.jpeg)

Go to: Where the World of Warcraft folder is located and installed

Select: World of Warcraft

Click: OK

Lutris Battle.net Runner and System Options

![](Images/image01146.jpeg)

Open: Lutris

Select: Blizzard Battle.net

Right Click: Blizzard Battle.net

Click: Configure

![](Images/image01147.jpeg)

Click: Runner options

Tick: Box in the same row as Show advanced options

Click: Box in the same row as Wine version

Click: WineHQ Staging

Move switches to the right for the following options

*   Enable DXVK
*   Enable D3D Extras
*   Enable Esync

Ensure that switches are located to the left for the following options

*   Enable VKD3D
*   Enable DXVK-NVAPI/DLSS

Click: Save

Manually Installing World of Warcraft Addons

Go to:

[https://www.curseforge.com/wow/](https://www.curseforge.com/wow/)

Click: Search Bar

Type In: Name of Addon or Scroll through the various categories

Choose an addon, for example Total Value

Click: Name of addon

Scroll down to recent files

Click: The Download button Under Recent Files, that is next to the version of World of Warcraft which the addon is being installed for

For example, WoW Retail

To Download TotalValue_Shadowlands_V1.1.1.zip

Go to: Where TotalValue_Shadowlands_V1.1.1.zip is downloaded

Double Click: TotalValue_Shadowlands_V1.1.1.zip

Select: TotalValue_Shadowlands

Click: Extract

Go to:

World of Warcraft/_retail_/Interface/AddOns

Click: Extract

World of Warcraft Addon Managers

*   Ajour

▪ Ajour

▪ Ajour Delete Addon

▪ Ajour Delete Variable

▪ Ajour Install Addons

▪ Ajour New Addon Directory

*   Strongbox

◦ Strongbox

◦ Strongbox Change Theme

◦ Strongbox Delete Addon

◦ Strongbox Delete Multiple Addons

◦ Strongbox Install Addon

◦ Strongbox Install Multiple Addons

◦ Strongbox New Addon Directory

*   wowmatrix

◦ wowmatrix

◦ wowmatrix Delete Addon

◦ wowmatrix Delete Multiple Addons

◦ wowmatrix Install Addon

◦ wowmatrix New Addon Directory

*   Wowup

◦ Wowup

◦ Wowup Delete Addon

◦ Wowup Delete Multiple Addons

◦ Wowup Install Addon

◦ Wowup New Addon Directory

Ajour

![](Images/image01148.jpeg)

Go to:

[https://github.com/ajour/ajour/releases/tag/1.3.2](https://github.com/ajour/ajour/releases/tag/1.3.2)

Click: ajour-opengl.AppImage

To: Download ajour-opengl.AppImage

Go to: Where ajour-opengl.AppImage is downloaded

Double Click: ajour-opengl.AppImage

![](Images/image01149.jpeg)

Click: Integrate and run

Ajour Delete Addon

![](Images/image01150.jpeg)

Open: Ajour

Click: My Addons

Click: Addon

Click: Delete Master Plan

![](Images/image01151.jpeg)

Click: Confirm deletion

Ajour Delete Variable

![](Images/image01152.jpeg)

Open: Ajour

Click: My Addons

Click: Addon

Click: Delete SavedVariables

![](Images/image01153.jpeg)

Click: Confirm deletion

Ajour Install Addon

![](Images/image01154.jpeg)

Open: Ajour

Click: Catalog

Click: Search Box

Type In or Copy and Paste:

master plan

Click: Install in the same row as Master Plan

Ajour New Addon Directory

![](Images/image01155.jpeg)

Open: Ajour

Click: Select Directory

![](Images/image01156.jpeg)

Go to: World of Warcraft folder

Click:

_retail_

_classic_

_classic_era_

Click: Interface

Select: Addons

Click: OK

Strongbox

![](Images/image01157.jpeg)

Go to:

[https://github.com/ogri-la/strongbox/releases/tag/5.0.0](https://github.com/ogri-la/strongbox/releases/tag/5.0.0)

Click: strongbox

To: Download strongbox

Go to: Where strongbox is downloaded

Double Click: strongbox

![](Images/image01158.jpeg)

Click: Integrate and run

Strongbox Change Theme

![](Images/image01159.jpeg)

Open: Strongbox

Click: View

Click: Dark Theme

Strongbox Delete Addon

![](Images/image01160.jpeg)

Open: Strongbox

Click: installed

Select: BlizzMove

Right Click: BlizzMove

Click: Delete

Click: OK

Strongbox Delete Multiple Addons

![](Images/image01161.jpeg)

Open: Strongbox

Select: Multiple Addons with Shift and Left Click

Right Click: A selected Addon

Click: Delete

Click: OK

Strongbox Install Addon

![](Images/image01162.jpeg)

Open: Strongbox

Click: Search

Click: Search Box

Type In or Copy and Paste:

Blizzmove

Click: install in the same row as BlizzMove

Strongbox Install Multiple Addons

![](Images/image01163.jpeg)

Open: Strongbox

Click: search

Click: Search box

Select: Multiple Addons to Install With Shift and Right Click

Click: Install selected

Strongbox New Addon Directory

![](Images/image01159.jpeg)

Open: Strongbox

Click: File

Click: New addon directory

![](Images/image01156.jpeg)

Go to: World of Warcraft folder

Click:

_retail_

_classic_

_classic_era_

Click: Interface

Select: Addons

Click: OK

wowmatrix

![](Images/image01164.jpeg)

Go to:

[https://www.wowmatrix.com/download](https://www.wowmatrix.com/download)

Click: FREE Download for Linux 64-bit

To: Download wowmatrix.tar.gz

Go to: Where wowmatrix.tar.gz is downloaded

Double Click: wowmatrix.tar.gz

![](Images/image01165.jpeg)

Select: wowmatrix

Click: Extract

![](Images/image01166.jpeg)

Go to:

/home/mylinuxmintpc/Applications

Click: Extract

wowmatrix Delete Addon

![](Images/image01167.jpeg)

Open: wowmatrix

Select: BetterWardrobe

Click: Uninstall

![](Images/image01168.jpeg)

Click: Delete Permanently

wowmatrix Delete Multiple Addons

![](Images/image01169.jpeg)

Open: wowmatrix

Select: NeatPlates_Slim_Horizontal and NeatPlates_Slim_Vertical

With: Shift and Left Click

Click: Uninstall

wowmatrix Install Addon

![](Images/image01170.jpeg)

Open: wowmatrix

Click: Get MoreAddOns

Click: Search box

Type In or Copy and Paste:

armory

Select: Armory

Click: Install

wowmatrix New Addon Directory

![](Images/image01171.jpeg)

Open: wowmatrix

Go to: Drive World of Warcraft is located on

Select: World of Warcraft folder

Click: Open

![](Images/image01172.jpeg)

Choose: Whether to Accept or Decline

Wowup

![](Images/image01173.jpeg)

Go to:

[https://wowup.io/](https://wowup.io/)

Click: Download Now

To: Download WowUp-2.6.1.AppImage

Go to: Where WowUp-2.6.1.AppImage is downloaded

Double Click: WowUp-2.6.1.AppImage

![](Images/image01174.jpeg)

Click: Intergrate and run

Wowup Delete Addon

![](Images/image01175.jpeg)

Open: Wowup

Click: My Addons

Select: Armory

Right Click: Armory

Click: Remove

![](Images/image01176.jpeg)

Click: Yes

Wowup Delete Multiple Addons

![](Images/image01177.jpeg)

Open: Wowup

Click: My Addons

Select: Multiple Addons

Right Click: One of the Addons selected

Click: Remove

![](Images/image01178.jpeg)

Click: Yes

Wowup Install Addon

![](Images/image01179.jpeg)

Open: Wowup

Click: Get Addons

![](Images/image01180.jpeg)

Click: The search bar

Type In or Copy and Paste:

armory

Press: ENTER

Click: Install in the same row as Armory

Wowup New Addon Directory

![](Images/image01181.jpeg)

Open: Wowup

Click: Options

Click: Clients

Click: Add New

![](Images/image01182.jpeg)

Go to: World of Warcraft/_retail_

Click: Wow.exe

Click: Open

or

Go to: World of Warcraft/_classic_

Click: WowClassic.exe

Click: Open

or

Go to: World of Warcraft/_classic_era_

Click: WowClassic.exe

Click: Open

About The Author

The Author of this self-help learning book graduated from The University of Buckingham with a degree in Business and Communications and now lives in the family home in the United Kingdom.

This is the authors eleveneth literary work with additional material in the planning stages, with subsequent works that hope to make beings and organizations happier.

Bibliography

The books written by the author, with the most recent going first:

*   Linux Mint 20.03 Self Help After Install Guide, 2022
*   Windows 11 After Install Self Help Guide, 2022
*   openSUSE Tumblweed After Install Self Help Guide, 2022
*   Debian 11 Bullseye After Install Self Help Guide Remastered, 2021
*   Ubuntu 20.04 LTS Self Help Guide Remastered, 2021
*   Linux Mint 20.XX Self Help Guide, 2021
*   Pop OS 20.04 Self Help Guide, 2021
*   Debian 11 Augment Self Help Guide, 2021
*   Ubuntu 20.04 LTS After Install Augment Self Help Guide, 2021
*   Debian 11 After Install Self Help Guide, 2021
*   Ubuntu 20.04.03 LTS After Install Self Help Guide, 2021