![](cover.jpeg)

![cover](cover.jpeg)

How to Build a

        Home or Office Web Server

By Stuart Gregory

Learn how to....

*   Configure your home network
*   Assign static IP addresses
*   Select & build hardware
*   Build a virtual private server (VPS)
*   Build a dedicated server
*   Install CentOS from DVD Rom
*   Create bootable USB pen drives
*   Install CentOS from USB pen drives
*   Use open source software
*   Install & configure software
*   Install & configure cPanel
*   Configure & Install server security
*   Assign domain names to your server
*   And much more

How to build a home or office web server

ISBN: 978-1-291-90720-9

Copyright © Stuart Gregory 2013

The right of Stuart Gregory to be identified as the author of this

works has been asserted in accordance with sections 77 and 78

of the Copyright Designs and Patents Act 1998.

Condition of sale

This book is sold subject to the condition that it shall not,

by way of trade or otherwise, be lent, re-sold, hired out or

otherwise circulated in any form of binding or cover other

than that in which it is published and without a similar

condition including this condition being imposed

Acknowledgements

With thanks to my loving wife and daughter for all the help and support enabling to write this book.

Table of Contents

[Chapter One](#part0000_split_003.html__Toc357428740)

[Static or Dynamic IP addresses](#part0000_split_004.html__Toc357428741)

[Choosing your Internet Service Provider (ISP)](#part0000_split_005.html__Toc357428742)

[Configuring your home network](#part0000_split_006.html__Toc357428743)

[Networking equipment](#part0000_split_007.html__Toc357428744)

[Hub configuration](#part0000_split_008.html__Toc357428745)

[Configure hub 1](#part0000_split_008.html__Toc357428746)

[Configure hub 2](#part0000_split_008.html__Toc357428747)

[Network port switch](#part0000_split_008.html__Toc357428748)

[Chapter Two](#part0000_split_009.html__Toc357428749)

[Virtual private servers (VPS)](#part0000_split_010.html__Toc357428750)

[Virtualisation](#part0000_split_010.html__Toc357428751)

[Host server](#part0000_split_010.html__Toc357428752)

[Dedicated servers](#part0000_split_011.html__Toc357428753)

[Chapter three](#part0000_split_012.html__Toc357428754)

[Server Hardware](#part0000_split_013.html__Toc357428755)

[Main server hardware](#part0000_split_013.html__Toc357428756)

[Pre built systems](#part0000_split_015.html__Toc357428757)

[Using an old PC](#part0000_split_016.html__Toc357428758)

[Additional hardware](#part0000_split_017.html__Toc357428759)

[Chapter four](#part0000_split_018.html__Toc357428760)

[About CentOS](#part0000_split_019.html__Toc357428761)

[Downloading CentOS](#part0000_split_019.html__Toc357428762)

[uTorrent](#part0000_split_020.html__Toc357428763)

[Image burn](#part0000_split_021.html__Toc357428764)

[CentOS bootable USB Pen Drive](#part0000_split_022.html__Toc357428765)

[Windows Bootable USB drive](#part0000_split_023.html__Toc357428766)

[Chapter five](#part0000_split_024.html__Toc357428767)

[Installing CentOS 6.3 from a DVD Rom Disc](#part0000_split_025.html__Toc357428768)

[Installing CentOS 6.3 from a Bootable USB](#part0000_split_026.html__Toc357428769)

[Create custom hard drive layout](#part0000_split_027.html__Toc357428770)

[Configuring Internet Access](#part0000_split_028.html__Toc357428771)

[Chapter six](#part0000_split_029.html__Toc357428772)

[Building a dedicated server](#part0000_split_030.html__Toc357428773)

[Building Virtual Private Server](#part0000_split_031.html__Toc357428774)

[Installing the host operating system](#part0000_split_031.html__Toc357428775)

[Disabling sleep mode for Windows 8](#part0000_split_031.html__Toc357428776)

[Installing Virtualisation software](#part0000_split_031.html__Toc357428777)

[Creating a Virtual Machine (VPS)](#part0000_split_031.html__Toc357428778)

[Installing CentOS 6.3 from a Saved Image](#part0000_split_031.html__Toc357428779)

[Auto start VPS on server boot up](#part0000_split_031.html__Toc357428780)

[Chapter seven](#part0000_split_032.html__Toc357428781)

[Configuring CentOS](#part0000_split_033.html__Toc357428782)

[Adding additional IP’s to a VPS](#part0000_split_034.html__Toc357428783)

[Adding additional IP’s to a dedicated server](#part0000_split_035.html__Toc357428784)

[Chapter eight](#part0000_split_036.html__Toc357428785)

[Installing cPanel](#part0000_split_037.html__Toc357428786)

[Configuring cPanel](#part0000_split_038.html__Toc357428787)

[Adding a domain name](#part0000_split_039.html__Toc357428788)

[Chapter nine](#part0000_split_040.html__Toc357428789)

[Creating a wheel user and disabling root access](#part0000_split_041.html__Toc357428790)

[Changing your SSH port](#part0000_split_042.html__Toc357428791)

[Installing server firewall](#part0000_split_043.html__Toc357428792)

[Chapter Ten](#part0000_split_044.html__Toc357428793)

[Optimising MySQL](#part0000_split_045.html__Toc357428794)

[Change full text search min word length](#part0000_split_046.html__Toc357428795)

[Chapter Eleven](#part0000_split_047.html__Toc357428796)

[Technical support](#part0000_split_048.html__Toc357428797)

[Chapter Twelve](#part0000_split_049.html__Toc357428798)

[Software](#part0000_split_050.html__Toc357428799)

[Winrar](#part0000_split_050.html__Toc357428800)

[WinZip self extractor](#part0000_split_050.html__Toc357428801)

[ISO2USB](#part0000_split_050.html__Toc357428802)

[Windows 7 USB/DVD Download Tool](#part0000_split_050.html__Toc357428803)

[CentOS x86 64bit](#part0000_split_050.html__Toc357428804)

[Windows 8 64 bit Bit operating system](#part0000_split_050.html__Toc357428805)

[uTorrent](#part0000_split_050.html__Toc357428806)

[Image Burn](#part0000_split_050.html__Toc357428807)

[Putty: a free Telnet/SSH Client](#part0000_split_050.html__Toc357428808)

[Oracle Virtualbox](#part0000_split_050.html__Toc357428809)

[cPanel](#part0000_split_050.html__Toc357428810)

# Chapter One

| In this chapter you will learn about static or dynamic IP addresses for web servers, choosing your internet service provider (ISP) and configuring your home network to run a home or web server. |

## Static or Dynamic IP addresses

In order to run a web server no matter if this is from home or a datacenter the World Wide Web needs to know where that web server is. This is done with an IP address. An IP address is like the phone number of where your server can be found.

Dynamic IP address change each time your router is turned off and on again. If your were to run a web server on a dynamic IP address then each time your router was turned off and back on you would have to configure your server, name servers and domain name to the new IP address. This would then result in new DNS propagation being needed and your web site and server could be offline for up to 24 hours while new DNS propagation takes place.

There are a few services on the market that lets you use dynamic DNS management to point your domain name to your home dynamic IP address; a small monthly fee is normally required. With these each time your routers IP is changed it will update and start the processes to point your domain name to your new dynamic IP. These services still result in some down time but most of the configuration is produced automatically.

If you wish to install cPanel, which is a server interface that lets you add and manage domain names on your server, then you will require a static IP address. The cPanel licence is only granted to static IP addresses.

A static IP address means that no matter how long or how often your router is turned off, when it re-boots your IP address will always be the same.

Some internet service providers offer single or multiple IP addresses for a small monthly fee. Most virtual private servers, (VPS) use only a single IP address, whereas most dedicated servers have at least two IP addresses assigned to them.

When hosting a website it is better to use static IP addresses as this means you are not sharing your IP address. Another person or company could have been using the dynamic IP address and sending out lots of email spam causing the IP address to be on a blacklist.

For the small charge and stability I would recommend using static IP addresses. For the examples in this book I have used an internet service provider (ISP) which has assigned 5 static IP addresses to my broadband connection. This will allow me to create 3 virtual private servers each with a single IP address and a dedicated server with two IP addresses assigned to it.

## Choosing your Internet Service Provider (ISP)

Choosing your internet service provider is the first part in building a home web server. Careful consideration needs to be implemented before signing up to an internet service provider. Once you have signed up you will be in a 12 or 14 month contract so choosing the right company first time is essential.

For the purpose and examples in this book I have chosen BT Business broadband. They offer fast fibre broadband and static IP addresses. BT Business broadband is happy for you to run a web or gaming server from their equipment and offer some support in configuring their router to allow this.

You don’t need to have business premises or be a business to have BT Business broadband installed as these can be installed in your own home. I have changed to have this installed in my home for the purpose of writing this book.

With BT Business broadband they offer a free business hub, I have two of these for this example but only one is required. I have also opted for the 5 static IP addresses.

## Configuring your home network

Once you have your broadband active and your static IP addresses assigned to your line you are ready to start configuring your hub ready for your home web servers. Their support only shows how to configure the hub to allow one web server to run with one static IP address assigned to that web server. In the examples we show in this book we are going to run multiple web servers and a dedicated server with multiple static IP addresses assigned to it; for this we will need to configure the hub and network differently to the way they show.

## Networking equipment

The networking equipment I am using in these examples are listed below. You may wish to use the same our substitute with your own equipment.

*   Two BT Business hubs
*   Network port switch
*   Multiple cat5 (Ethernet) cables

Only one BT Business hub is required for the servers but as I want to connect my home PC to this broadband line and have it protected by the routers firewall, I have the second hub configured to allow my home computers protected access.

## Hub configuration

### Configure hub 1

We will configure hub 1 first, this hub will act as a gateway hub for all internet traffic and access to the servers. To access your hub you will need to connect you computer to the hub via a cat5 Ethernet cable. To access the hub open a browser and type 192.168.1.254 in the browser URL address bar.

This will open your new hub for first time settings. As the hub is new it will ask you to enter the admin password and set a new admin password. The factory set password is located on the little pull out tab on the back of the hub.

Once you have set your admin password and gained access to your hub you need to select settings then advanced settings for the menu bar. Next, click continue to advanced settings.

There are only a few simple steps to configure this hub and the first step is to disable the wireless connection. The reason why we are going to disable the wireless connection is because this hub will act as a gateway only so we don’t want home computers connecting to this hub directly.

Click on the wireless tab in the menu bar and follow the on screen instructions to disable the wireless connections.

Next is to allow static IP addresses. Select the static IP option on the menu bar. This will open up a new window with four options. Select on for the first option of static IP address, next you will need to enter the router IP address; this would have been sent to you in your welcome letters regarding static IP address. Next we need to select our subnet mask. As I have ordered 5 static IP addresses I select the subnet mask which ends in .248, your subnet mask will also be on the welcome letters regarding static IP addresses, finally under this section we need to make sure that ‘allow incoming ping requests’ is set to yes. Click ‘apply’ and your static IP addresses are now activated.

The last thing we need to do under hub 1 is to deactivate the firewall and allow all incoming traffic. From the options menu bar click port forwarding and then from the sub menu click firewall.

Once the new page opens you will need to select disabled and then apply.

Hub 1 is now configured to allow all incoming connections which will be routed later on to the appropriate server.

### Configure hub 2

If you are not using a second hub for your home computers then you can skip this step.

For this step I connected to hub 2 via the wireless option on my home computer, but you could use a cat5 Ethernet cable again. Once you have entered the settings and password to connect your computer wirelessly to hub 2 you can enter 192.168.1.254 in the browser URL address bar. You will also need to set the admin password for hub 2 like you did before for hub 1\. I would recommend setting a different password for hub 2 that way you are always sure which hub you are connecting to.

Once you have set the admin password and gained access to hub 2 we have just a few settings to configure. You will need to navigate to advanced setting > business network and then IP address from the sub menu.

Once that page is opened we will change the hub IP gateway address. I have changed mine from ending in .254 to end in .10, this will allow both hubs to be accessed independently from a browser.

Next we need to set DCHP server to no. If this is not set to no then both hubs would not communicate correctly with each other, click apply to save the new settings we have made.

You will most probably need to restart you computer at this point so that your computer picks up the new settings as well.

Connect your hub 2 to hub 1 via a cat5 Ethernet cable. Connection should be made from Ethernet port 1 on hub 1 to Ethernet port 1 on hub 2\. This will allow hub 2 to receive broadband from hub 1.

You should now be able to login to hub 2 from the new hub IP address by entering 192.168.1.10 in the browser URL bar. You will also be able to login to hub 1 with the hub IP 192.168.1.254 when entered in the browser.

You should now have both hubs correctly configured to allow internet to your servers and wirelessly to your home computers. On hub 1 you will now see the power light and the broadband light active. On hub 2 you will see the power light and the wireless light active.

### Network port switch

As we are going to assign multiple static IP addresses to our dedicated server and require static IP addresses to our virtual private servers we are going to use multiple cat5 Ethernet cables so it may be a good idea to buy a network port switch. This will allow you to take one cat5 Ethernet cable and split this into a number of other cat5 Ethernet cables. In this example I am using an 8 port network switch.

The network port switch allows one cable from hub 1 into the Ethernet port 1 on the network switch; this then gives the broadband internet to the network switch and in my case 7 more Ethernet cables to be connected directly to the servers.

As we disabled the firewall on hub 1, which is the hub that all our servers intend to be connected to it would be a good idea for security to purchase a separate firewall which can be connected in line before the network port switch. I have not done so in this example but in reality I would. This can be purchased on the internet and range in price from a few pounds to a few thousand pounds.

# Chapter Two

| In the chapter you will learn what a virtual private server (VPS) is, what a host server is, what a dedicated server is and what the differences between them are. We will also cover the operating systems and software that we will be using to create our virtual private server (VPS) and dedicated server. |

## Virtual private servers (VPS)

A virtual private server (VPS) is a virtual machine which with the aid of software runs in the same physical server as many other virtual machines.

Despite the virtual machine residing within another larger server it still can be configured to run independently of all other virtual machines.; thus meaning it can be totally configured to each customers individual needs and has the complete privacy of an independent server.

Many web servers will process a website request and return the result to the end user, in some and almost all cases websites can have a long inactive period where no load is placed upon the server. Creating virtual private servers allows other servers on that machine to utilise this dead load time.

### Virtualisation

When we talk about creating one machine and producing virtual machines (VPS) from that we are actually using virtualisation software to do this. By creating one host computer with hardware that supports virtualisation we can then create smaller independent computers within the hosts via the use of the host’s hardware.

This has become a very large concept within the web hosting industry, allowing large amounts of servers to be created at cheaper costs; requiring less space, hardware and power consumption.

### Host server

The host server plays a key concept in creating and running our virtual private servers. The host server allows you control over all virtual machines, creating new, stopping, starting and suspending virtual machines.

A host server can run on Windows or Linux, for the examples in this book we are going to install windows 8 on our host server. I have chosen this as most home users are familiar with Windows operating systems and will find managing their virtual machines much easier with such a familiar environment.

Once Windows is installed on the host server, virtualisation software needs to be installed so that our virtual machines can be created. There are many virtualisation software programs available and we have chosen Oracle’s Virtualbox (open source software).

Virtualbox is an extremely powerful x86, AMD64 and Intel64 virtualisation software which can be used for home, business and large enterprise solutions. Virtualbox is extremely feature rich and serves as a high performance software.

For more information about Oracle’s Virtualbox please visit

[https://www.virtualbox.org](https://www.virtualbox.org)

Once we have our host server running Windows and Virtualbox installed we are ready to create our first virtual private server. We will cover installing and configuring our software later in the book.

## Dedicated servers

A dedicated server is a single physical computer in which the user has the full system resources at their disposal. Dedicated servers are more expensive but have the advantage of that you are not sharing your physical resources with another server.

Setting up a dedicated server is much quicker as you would not need the host server and virtualisation software like when creating a virtual private server (VPS).

CPanel licences are required to install and use CPanel software on your server. This is the only monthly fee (other than your internet service providers cost for broadband and IP addresses.) that will be required. CPanel licences can be purchased monthly from a variety of sources on the internet all at roughly the same cost. Licences for dedicated servers are roughly three times the price for that of a virtual private server but each gives you the same software and control.

Virtual server licence         £10 monthly

Dedicated server licence              £26 monthly

# Chapter three

| In this chapter we will cover the hardware needed to create our virtual private server (VPS) and our dedicated server. This will cover selecting the hardware and using an old desktop PC as a server. |

## Server Hardware

There is an extreme amount of computer hardware on the market today and selecting the correct hardware for you needs can become very confusing. For the examples in this book we are going to choose from the slightly higher end of the market to create a powerful server yet we are going keep our budget at £400 for each.

The server hardware we are selecting can create a dedicated server of 8 cpu cores, 16gb ram and a 1tb hard drive. Or we can create a host operating system and 7 virtual private servers of 1 cpu core, 2gb ram and 100gb hard drive.

There is some additional hardware required such as a PC monitor and we will cover these shortly.

### Main server hardware

The main hardware we are going to require to build each of our dedicated servers and our virtual private servers are:

*   Motherboard
*   Processor, fan and heat sink
*   Thermal paste
*   PC case and power supply
*   Hard drive
*   Memory

Because I wanted to make sure that all these parts are available to all readers of this book I purchased all these parts from eBay. There are a large number of sellers who advertise motherboard bundle deals which include the motherboard, memory, Processor, fan and heat sink. These are priced between £200 - £300\. This leaves you with just the hard drive, case, power supply unit and thermal paste to purchase.

I have chosen to boot my operating system from USB which eliminates the need for a DVD Rom drive. If you would like to install and boot your windows and centos for disc then you will also require a DVD Rom drive.

The hardware I selected for both my dedicated and virtual private servers is:

Motherboard

Asus M5A78L-M/USB3

This motherboard supports AMD and AM3+multi-core processors, it also delivers better overclocking capabilities with much less power consumption. The memory support is dual-channel DDR3 NON-ECC up to 16gb.

The form factor is Micro ATX which allows me to choose a slim line case with good cooling. It has two PCI slots which will allow me to add additional 10/100/1000 (gigabyte) Ethernet cards.

The motherboard CPU socket is AM3+ which means that the processor that is chosen must also be AM3+

The only really drawback of this motherboard is that it is only SATA II -3Gb/s whereas most of the new hard drives are now SATA III – 6Gb/s. This just means that my hard drive won’t run at its full potential.

Processor

AMD FX Black Edition 8 Core Processor socket AM3+

As the motherboard is socket AM3+ this means that the socket of the processor must also be AM3+ in order to fit.

This is part of the new AMD FX black edition range which comes unlocked ready for overclocking. The main points about the processor is that it uses AMD Virtualisation technology which means it is perfect for creating our virtual private servers.

When buying a new processor they will always come with the heat sink and CPU fan. If you are purchasing a used processor then you must check that they come with a heat sink and fan.

I would recommend that you should buy new, processor pins can be damaged when removing them or if poorly packed rendering them useless. Over used processors can also result in poor performance.

Memory

Corsair Memory 4GB DDR3 1333 Mhz dual channel

This memory is pretty compatible with most systems and is almost the cheapest on the market. Just because it’s cheap does not show in its performance.

The motherboard I have selected can take four of these memory sticks giving me a total of 16gb memory for each system.

Hard drive

Seagate 1TB hard drive SATA III 6Gb/s 64mb cache

There’s not much to say about the hard drive. There are a few to select from but I like Seagate hard drives. They have always been reliable for me.

Hard drives now go up to 4tb so feel free to select the hard drive size that will be best for you. If you are running a gaming server or file sharing server then maybe a bigger drive would be better. If you just intend to run a simple web server then a 1tb would be more than adequate.

Thermal paste

4g arctic cooling thermal paste

Thermal paste is used to bind the processor to the heat sink. You only use about a pea size on the heat sink and then spread it around. Too much thermal paste can be dangerous as it can leak over and onto the motherboard. For these two machines you would only need about a 1g tube but I could only find a 4g tube.

Case and power supply

Silverstone Milo micro ATX with 400w PSU

Choosing the right case can be very tricky. There are so many in look and functionality yet very few jump out and say that’s right for me. There are some things to consider before you order the case and power supply unit (PSU).

*   Size (where is the case going?)
*   Cooling (does the case have extra fans?)
*   Power supply output (is the wattage high enough?)

Size is very important. As the case I have selected can fit a micro ATX motherboard then it seems ok. But does it fit where I would like to place the server? Have a look at the overall size of the case. You will need to add 75mm to the rear of the case in order to allow for the power supply cable and all other cables that will be connecting to the rear of the case.

If you intend to boot your operating systems from a USB pen drive then it would be a good idea to make sure that the case has front USB drives.

Ventilation is a must when the server is intended to be running 24/7\. Allowing a gap all the way around the case to allow the extra fans to function and air to circulate is critical.

Cooling is of high importance. The processor comes with one fan but the motherboard supports one additional case fan. We would need at least one case fan as a must. Two would be better. Make sure your case has room for a case fan if it does not already come with one installed.

Power supply unit (PSU) with the hardware selected above the power consumption would be around 200w. For the sake of caution I would opt for a minimum of 300w power supply. This comes with a 400w so that’s ok

## Pre built systems

If you are not confident of selecting and installing the hardware yourself there are a number of pre built systems available on eBay or from your local computer supplier each that will meet the correct specifications.

If you are not sure if the pre built system does meet your needs you can always ask them giving them the specifications required; although most will list all the specifications in the item description.

Buying the system pre built will normally be slightly more expensive, (not much) and will take away the hassle of choosing the right hardware that’s compatible. These will come ready for you to connect your monitor and start installing your operating system.

## Using an old PC

If you are not sure if you are ready to take the jump to purchasing new equipment just yet and would like to try out the virtualisation software or create a standard dedicated server then old laptops or desktop computers are perfect for this.

If you just want to create a dedicated server from an old desktop or laptop then as long as you have a computer that has at least 1gb memory and 50gb or more hard drive then you should be ok and can go and create your CentOS disc or bootable USB stick ready to install.

This would only give you a low performance dedicated server but it would be enough to get CentOS and CPanel installed ready to connect your new server to the internet.

For creating a virtual private server from an old desktop or laptop then you would need at least 3gb memory, 100gb hard drive and at least a dual core processor.

Windows would require 2gb memory and 1 core processor to boot up and the virtualisation software is then installed on the windows platform. I first tried this out on an old HP laptop running Windows XP; it was a slow laptop but worked well, enough to get the hang of the virtualisation software. I had the VPS server that I created CentOS and CPanel installed up and running in less than a day. I then added a website to this which I kept online for about three days in order to check stability and functionality.

I then got an old desktop for £50 which I used to create a dedicated server and did similar with that; installed CentOS and CPanel then a website. Once I was sure that stability and functionality were there I choose to purchase the hardware to make more advanced dedicated and virtual private servers.

From this I then went on to create a small office network of servers through to a mini data centre of around 80 servers.

## Additional hardware

Depending on your requirements and how many servers you intend to create and install you will also want to consider the following hardware.

*   USB pen drives.
*   DVD Rom drives
*   Network port switch
*   Cat5 or Cat6 Ethernet cables
*   KVM switch

If you intend to boot your operating systems from DVD discs then you will require a DVD Rom for each server. I opted to boot mine from USB pen drives as this then allows for less hardware and power consumption. Also as the drive will only be required once in a blue moon I felt that this was unnecessary.

A USB pen drive can be transferred from server to server with ease. As I will be using the pen drive to boot windows 8 and CentOS I purchased two 8gb pen drives to create bootable operating systems and a third 8gb pen drive for transferring any drivers or files across.

A network port switch will allow you to bring one Ethernet cable to the switch from your hub and then split to allow each server to have the required Ethernet connections on the LAN ports. These can be purchased on eBay for around £12 plus delivery. This would get you an 8 port network switch, one LAN port for your Ethernet connection from your gateway hub, and then an additional 7 LAN ports to connect your servers.

As in this book I am going to create a host server and a dedicated server I only want to use one monitor, keyboard and mouse. This is where the KVM switch comes into use. A KVM switch stands for keyboard, visual graphics adapter and mouse. The USB versions are relatively cheap on eBay costing around £15 for a 4 port USB KVM Switch. As this is a USB KVM switch a USB keyboard and mouse is required.

Cat5 Ethernet cables are for 100mb data transfer and Cat6 Ethernet cables are for Gigabyte data transfer. Depending on your network switch select the appropriate additional cables you will require.

# Chapter four

| In this chapter we will cover about CentOS, downloading and creating your CentOS 6 DVD and Bootable USB ready for installation. |

## About CentOS

CentOS (Community Enterprise Operating System) is a Linux based operating system and is used by a large majority of servers around the world. CentOSis open source which means it’s free.

### Downloading CentOS

To download CentOS you can either download directly or download the torrent file and open it with the likes of uTorrent (open source software) to download the file. As the CentOS discs are large files I prefer to download the torrent file.

Please see our software chapter for the download location.

From that web page you can select your mirror site to download CentOS 6.3 from. I used the first one on the list. This opens up in a new web page. On this web page you will see a list of file names. We need DVD 1 only but for speed I downloaded the file CentOS-6.3-x86_64-bin-DVD1to2.torrent and opened this in uTorrent to start my download.

Once the download is completed you will need to burn the ISO file to a DVD disc. Remember we only need to use DVD 1 for our examples. To burn the ISO file to disc I used image burn which again is open source software.

If you require any help with download and using uTorrent or image burn please see the sections below.

## uTorrent

Please see our software chapter for the download location.

When you have opened the uTorrent web page click get uTorrent, this will open a new page for you to select the uTorrent version.

All we need is the free version so click free download, this will refresh your page and start your download. There is also on screen instructions for installing uTorrent.

Your CentOS DVD 1 to 2 download will take some time depending on your broadband speed so please be patient. Once completed you will now have a folder called ‘CentOS’ in your downloads folder or where you have selected uTorrent to store your downloads.

## Image burn

Please see our software chapter for the download location.

Do not click on any of the download buttons on the page that opens. Most of these are paid advertisements and will take you to other websites. On the menu bar at the top of the page you will see, News | Download | Change log

Click on Download, this will take you to a new page with a list of mirror sites to start a download from. I used the second mirror site on the list which when opened has a big blue box for download now on the right had side of the page. This then begins your imgBurn download.

Once downloaded you double click and follow the onscreen prompts to install image burn.

Once image burn has been installed open your CentOS folder that has been downloaded and right click on the CentOS DVD 1 .img file, select open with ImgBurn.

This will now prompt you to enter your blank DVD and start your burn to disc.

## CentOS bootable USB Pen Drive

Once you have your CentOS ISO image file you can use this to create a bootable USB drive. You will need software for this. I used the open source software ISO2USB for CentOS/RedHat.

This is free software and very simple to use. It will install a bootable version of CentOS on your pen drive in about 10 minutes. You can then use this bootable pen drive on all your servers time and time again.

Please see our software chapter for the download location.

Once downloaded you will need to extract the file contents with Winrar or WinZip to your chosen file location

You will now see an ISO2USB image incon in your chosen folder. Double click on this to open the program.

![iso2usb.png](images/00001.jpeg)

Make sure the Diskimage button is clicked and leave this set to ISO and select the ISO file location, which in this case will be the CentOS DVD Rom Disc one we downloaded previously.

Leave the Hard Disk name and USB Device name as they are which should be sda.

Select your USB Drive and the Drive location. This will most probably all ready be selected for you. Click ok and this will now create your bootable CentOS USB pen drive.

## Windows Bootable USB drive

As we will be using Windows 8 as the host operating system we will also need to create a bootable USB pen drive for this.

First with your Windows 8 operating system disc you will need to create an image file on your computer. Open image burn and select ‘create image file from disc’.

Make sure you have inserted your Windows 8 DVD disc into your DVD writer and select the location on your computer to store the image file. Click the ‘Read’ button on the bottom of Image burn and this will create your ISO image file.

From this image file you can now create your bootable USB pen drive.

There are other programs that can create this but I stuck with a Microsoft program which is the Windows 7 USB DVD download tool.

Please see our software chapter for the download location.

Don’t worry this will create other bootable Windows operating system discs. Once downloaded follow the on screen instructions and create your Windows 8 bootable USB pen drive.

This is a self extracting Microsoft program. Find the download in your downloads folder and double click.

![snipping_1.PNG](images/00002.jpeg)

Once the previous image loads select run to start your installation.

The next image will be the welcome screen. Click next

![snipping_2.PNG](images/00003.jpeg)

![snipping_3.PNG](images/00004.jpeg)

We are now ready to install Windows 7 USB/DVD download Tool. Once you click ‘Install’ the program will start the installation screen, depending on your computer it will only take a few seconds to install.

![snipping_4.PNG](images/00005.jpeg)

When the ‘Completed the Windows 7 USB/DVD Download Tool Setup Wizard’ screen appears click ‘Finish’ to exit the installer.

You will now have the Windows 7 USB DVD download tool icon on your desktop. Double click this to open the program.

![snipping_5.PNG](images/00006.jpeg)

Click ‘Browse’ to select the location of your Windows 8 ISO file you created earlier.

![snipping_6.PNG](images/00007.jpeg)

Next we need to choose our media type. Click ‘USB device’.

![snipping_8.PNG](images/00008.jpeg)

You should now see your USB device selected and available storage. If you have files on your USB pen drive I would recommend backing them up as the tool will reformat the USB pen drive.

![snipping_9.PNG](images/00009.jpeg)

The Windows 7 USB/DVD download tool will now format the USB pen drive and copy the files needed across. This will take about 10 to 15 minutes depending on your computer.

# Chapter five

| In this chapter we are going to install our CentOS 6.3 Operating system from both DVD Rom and Bootable USB pen drive. We will then configure CentOS for internet access and assign a static IP address to the server. |

## Installing CentOS 6.3 from a DVD Rom Disc

Now that we have our dedicated server hardware ready and our CentOS 6.3 DVD 1 on disc we can start with installing the server base operating system.

Select your server to boot from CD and insert your CentOS DVD 1 in your DVD Rom drive.

![centos_1.jpg](images/00010.jpeg)

Once the above screen shot loads you will need to select install or upgrade an existing system.

The next screen to appear is to begin testing the media before installation. Choose skip to skip the media test and start the installation.

Testing the media does take some time and there should not really be a problem with the installation media so you will be ok to skip this test and start the installation off your CentOS 6.

![centos 2.png](images/00011.jpeg)

The welcome screen of CentOS will now be displayed. Click next of the screen that appears as below.

![centos_3.png](images/00012.jpeg)

You will now be asked to select your keyboard language for your CentOS installation. As per the screen shot below.

![centos_4.png](images/00013.jpeg)

After clicking next on select you language you will be presented with the screen as per below, select you keyboard layout language.  For those that have installed operating systems before this will all seem very familiar.

![centos_5.png](images/00014.jpeg)

As with our server build we are using a locally attached hard drive you should select basic storage devices on the following screen.

![centos_6.png](images/00015.jpeg)

You might see the following warning - Error processing drive. If you see this click on the Re-initialize  all button to proceed:

![centos_7.png](images/00016.jpeg)

The below message will also most likely appear stating that the below storage device may contain data. If this appears and you are confident that there is no data on the hard drive that needs backing up or keeping you may select ‘Yes, discard any data’.

A small box will appear for just a few seconds, maybe longer if you have a very large hard drive stating examining storage device.

![centos_7.1.PNG](images/00017.jpeg)

Once your hard drive is initialized and accepted as a suitable storage device you will be taken to the next screen to continue you installation.

You will now need to fill in the hostname of the server (e.g. server1.example.com), then click on the Configure Network button:

As this will be a web server which will most likely host your website it would be a better idea to replace example.com with your domain name. Hostnames must be a fully qualified domain name. It is acceptable to have server1\. or vps1\. But the hostname must end with a domain name.

![centos_8.png](images/00018.jpeg)

After the clicking the Configure Network button the network Connections window will popup. Select System eth0 and click edit to configure your network.

![centos_9.png](images/00019.jpeg)

After the edit button is selected a further popup box will appear as per below. Click on the connect automatically check box, and then on the IPv4 Settings tab.

Under the Method: dropdown box make sure that Automatic (DHCP) is selected and click on apply which will close the Editing System eth0.

![centos_10.PNG](images/00020.jpeg)

The reason why we are allowing automatic DCHP rather than setting the static IP address here is that each eth0 connection has its own mac address and we will be assigning the IP address later on in the BT gateway hub.

You will now need to click close the network connections box and they you will see a message appear as per below.

![centos_11.PNG](images/00021.jpeg)

Once the above message closes of your network connections are completed and you can proceed.

Depending on the speed of the server the message can only be displayed for a split second so you may miss it. As long as you don’t see any error messages then you will be ok to continue with the installation.

If waiting for network manager returns an error message this is most commonly an error message because you have not connected your server via the Ethernet cable to your network port switch or your gateway hub.

Make sure you have connected your Ethernet cable and try the settings again.

If you have multiple Ethernet ports on your server and are intending to use more than one you will need to perform these settings for each of the system eth0 ports.

When the screen is returned back to the below screen shot you can click next to continue the installation of CentOS.

![centos_12.png](images/00022.jpeg)

You now need to select your time zone; you can use the dynamic map or use the dropdown list to set your time zone. Click next when you have finished.

![centos_13.png](images/00023.jpeg)

When logging into your server the main username is always root. If you intend to install cPanel, to access the WHM panel and configure cPanel your username will be root along with the password you select here. Your main username for SSH connections will be root and the password you select here.

Here you will need to set a password for the root user. Servers that are connected to the outside world (World Wide Web) come under attack so setting a weak password here is not recommended. It is good practise to use a combination of upper and lower case letters along with a selection of numbers.

It will also be a good idea to write these details down now. The main user is always root and your password is what you choose now. Your root password must be at least six characters long.

![centos_14.png](images/00024.jpeg)

Next we do the partitioning. Select, use all space. This will give you a small /boot partition and a large / partition which is fine for most purposes.

If you intend to install cPanel on your server you will be best to create a custom layout. This is recommended by cPanel but not compulsory.  If you require this step please now read the chapter on create custom hard drive layout and return to continue your installation.

![centos_15.png](images/00025.jpeg)

You will now be asked to write changes to disk. Click the button selecting, write changes to disk.

![centos_16.png](images/00026.jpeg)

If you have selected review or modify partitioning layout you will see two additional screens. At this stage you do not need to modify any of the partitions as we will cover creating custom partitions in a separate section of this chapter.

You will now be presented with the partitioned drive structure. Click next.

![centos_16.1.PNG](images/00027.jpeg)

The hard drive will now be formatted with the required partitions.

![centos_17.PNG](images/00028.jpeg)

Click on next to confirm installation of the boot loader on the selected partition.

![centos_17.1.PNG](images/00029.jpeg)

Next we need to select the software we want to install. Select Basic Server, then check CentOS in the additional repositories field, choose Customize laterand click on next.

![centos_18.png](images/00030.jpeg)

The installation of CentOS will now begin. This normally takes around 10 minutes to complete.

![centos_19.PNG](images/00031.jpeg)

When the installation has completed you can remove the DVD media from your Rom drive and click the reboot button.

![centos_20.PNG](images/00032.jpeg)

You have successfully installed CentOS basic server operating system on your server and it is now ready for you to configure and update.

After your server has rebooted you can login to CentOS with the username root and the password you created previously.

Next you will need to configure your installation for internet access. To do this please read the section configuring internet access at the end of this chapter.

## Installing CentOS 6.3 from a Bootable USB

When installing CentOS from a bootable USB drive there is not much of a difference in the installation but there are a few little differences. First you should insert your USB pen drive into a USB port turn on your server and select to boot from your USB device.

Once the below screen shot loads you will need to select install or upgrade an existing system.

![centos_1.jpg](images/00033.jpeg)

Unlike installing CentOS from a DVD the next screen that appears is the select language. The screen layout is also in a different format to that of booting via a DVD disc.

![20130416_083251_2.jpg](images/00034.jpeg)

After clicking next on select your language you will be presented with the screen as per below, select your keyboard layout language.

![20130416_083917_2.jpg](images/00035.jpeg)

Once you have selected your installation language and your keyboard you will have to select installation method. You will be asked what type of media contains the installation image.

Using your arrow keys on your keyboard highlight hard drive and select ok.

![usb.png](images/00036.jpeg)

When asked for partition that holds the image, this will most likely be /dev/sda1 from when we created our bootable USB drive previously. Select the drive and then ok.

![installerpartition.png](images/00037.jpeg)

Installation of CentOS will now start. Select the next button to continue.

![centos_3.png](images/00012.jpeg)

We are now installing CentOS identically as the boot from DVD Rom. If you have installed CentOS before via DVD Rom you will be familiar with the rest of the installation.

![centos_6.png](images/00038.jpeg)

You might see the following warning - Error processing drive. If you see this click on the Re-initialize all button to proceed:

![centos_7.png](images/00039.jpeg)

The below message will also most likely appear stating that the below storage device may contain data. If this appears and you are confident that there is no data on the hard drive that needs backing up or keeping you may select, Yes, discard any data.

A small box will appear for just a few seconds, maybe longer if you have a very large hard drive stating examining storage device.

![centos_7.1.PNG](images/00017.jpeg)

Once your hard drive is initialized and accepted as a suitable storage device you will be taken to the next screen to continue you installation.

You will now need to fill in the hostname of the server (e.g. server1.example.com), then click on the Configure Network button:

As this will be a web server which will most likely host your website it would be a better idea to replace example.com with your domain name. Hostnames must be a fully qualified domain name. It is acceptable to have server1\. or vps1\. But the hostname must end with a domain name.

![centos_8.png](images/00018.jpeg)

After the clicking the Configure Network button the network Connections window will popup. Select System eth0 and click edit to configure your network.

![centos_9.png](images/00019.jpeg)

After the edit button is selected a further popup box will appear as per below. Click on the, connect automatically check box and then on the IPv4 Settings tab.

Under the Method: dropdown box make sure that Automatic (DHCP) is selected and click on apply which will close the Editing System eth0.

![centos_10.PNG](images/00020.jpeg)

The reason why we are allowing automatic DCHP rather than setting the static IP address here is that each eth0 connection has its own mac address and we will be assigning the IP address later on in the BT gateway hub.

You will now need to click close the network connections box and they you will see a message appear as per below.

![centos_11.PNG](images/00021.jpeg)

Once the above message closes off your network connections are completed and you can proceed.

Depending on the speed of the server the message can only be displayed for a split second so you may miss it. As long as you don’t see any error messages then you will be ok to continue with the installation.

If waiting for network manager returns an error message this is most commonly an error message because you have not connected your server via the Ethernet cable to your network port switch or your gateway hub.

Make sure you have connected your Ethernet cable and try the settings again.

If you have multiple Ethernet ports on your server and are intending to use more than one you will need to perform these settings for each of the system eth0 ports.

When the screen is returned back to the below screen shot you can click next to continue the installation of CentOS.

![centos_12.png](images/00022.jpeg)

You now need to select your time zone; you can use the dynamic map or use the dropdown list to set your time zone. Click next when you have finished.

![centos_13.png](images/00023.jpeg)

When logging into your server the main username is always root. If you intend to install cPanel, to access the WHM panel and configure cPanel your username will be root along with the password you select here. Your main username for SSH connections will be root and the password you select here.

Here you will need to set a password for the root user. Servers that are connected to the outside world (World Wide Web) come under attack so setting a week password here is not recommended.  It is good practice to use a combination of upper and lower case letters along with a selection of numbers.

It will also be a good idea to write these details down now. The main user is always root and your password is what you choose now. Your root password must be at least six characters long.

![centos_14.png](images/00024.jpeg)

Next we do the partitioning. Select use all space. This will give you a small /boot partition and a large / partition which is fine for most purposes.

If you intend to install cPanel on your server your will be best to create a custom layout. This is recommended by cPanel but not compulsory.  If you require this step please now read the chapter on create custom hard drive layout and return to continue your installation.

![centos_15.png](images/00025.jpeg)

You will now be asked to write changes to disk. Click the button selecting write changes to disk.

![centos_16.png](images/00026.jpeg)

If you have selected review or modify partitioning layout you will see two additional screens. At this stage you do not need to modify any of the partitions as we will cover creating custom partitions in a separate section of this chapter.

You will now be presented with the partitioned drive structure. Click next.

![centos_16.1.PNG](images/00027.jpeg)

The hard drive will now be formatted with the required partitions.

![centos_17.PNG](images/00028.jpeg)

Click on next to confirm installation of the boot loader on the selected partition.

![centos_17.1.PNG](images/00029.jpeg)

Next we need to select the software we want to install. Select Basic Server, then check CentOS in the additional repositories field, choose Customize laterand click on next.

![centos_18.png](images/00030.jpeg)

The installation of CentOS will now begin. This normally takes around 10 minutes to complete.

![centos_19.PNG](images/00031.jpeg)

When the installation has completed you can remove the DVD media from your Rom drive and click the reboot button.

![centos_20.PNG](images/00032.jpeg)

You have successfully installed CentOS basic server operating system on your server and it is now ready for you to configure and update.

After your server has rebooted you can login to CentOS with the username root and the password you created previously.

Next you will need to configure your installation for internet access. To do this please read the section configuring internet access at the end of this chapter.

## Create custom hard drive layout

When installing Red Hat Enterprise Linux, it is recommended to use an ext file system (ext2, ext3, or ext4).

I have listed below the most common partition system for CentOS and a cPanel server configuration setup. There are more optional partitions you can add to these if your server requires them but this configuration is sufficient for the large majority of servers.

| /boot | 495MB |
| /temp | 2GB |
| swap | Twice the servers RAM |
| / | Grow to fill disk |

The /boot partition is used for the Karnels, boot loader and configuration files of your server.

The /temp partition is where all temporary files will be stored on your server.

The swap partition is used for the amount of RAM overflow that your system can write to your hard drive disk.

The / partition which is set to grow to fill disk is the main partition of your server and is where your base operation system is stored. cPanel will be installed here and create any required directories such as /home, /var and /usr.

In order to create a custom layout of your partitioning you will need to select create custom layout on the installation screen which type of installation would you like?

Once you have selected create custom layout as per the screen shot below click next. This will then take you into the edit and modify hard drive partitioning.

![centos_21.PNG](images/00040.jpeg)

You will now see your hard drive, named sda and the free space as per the screen shot below. If you see other partition volumes other than as shown delete these as these will be from previous installation on this hard drive.

![centos_22.PNG](images/00041.jpeg)

Highlight the free line under your sda hard drive and click on create at the bottom of your screen.

![centos_23.PNG](images/00042.jpeg)

On the small popup box that appears called create storage select standard partition and click create.

![centos_24.PNG](images/00043.jpeg)

First we will create the /boot partition. Under the Mount point: select /boot the file system type select box should already be set to ext4 but just make sure that this is set to ext4.

Under size (MB) is where you enter the size of the partition that you require. Here we enter 495\.

Under additional size options make sure fixed size is selected and click ok.

You will now see you /boot partition on your hard drives with a tick next to it.

![centos_25.PNG](images/00044.jpeg)

Highlight the line free again and we can now create our temp partition. When you have highlighted it click the create button at the bottom of your screen.

On the first popup box you will need to click standard partition again.

Under the Mount point: select /tmp, the file system type select box should already be set to ext4 but just make sure that this is set to ext4.

Under size (MB) is where you enter the size of the partition that you require. Here we enter 2048 which will give us the 2GB recommended.

Under additional size options make sure fixed size is selected and click ok.

![centos_26.PNG](images/00045.jpeg)

You will now see you /boot and /tmp partition on your hard drives with a ticks next to them.

![centos_27.PNG](images/00046.jpeg)

Next is to create the swp partition. Highlight the line free again. When you have highlighted it click the create button at the bottom of your screen.

On the first popup box you will need to click standard partition again.

Once the add partition popup box appears you will need to leave mount point blank and under file system type select swap.

The size (MB) will need to be set to twice your servers RAM. On my server I have allocated just 1GB of RAM so I will set this to 2048.

Under additional size options make sure fixed size is selected. Your add partition popup box should look like the screen shot below.

![centos_28.PNG](images/00047.jpeg)

Click ok which will return you to the screen showing your hard drive partitions.

![centos_29.PNG](images/00048.jpeg)

We now need to create our last partition which is to fill all remaining space of the hard drive. Again we need to select the line free and click on create. On the first popup box select standard partition again and click the create button.

Under mount point select / and again the file system type should already be ext4 but just check. Under additional size options select fill to maximum allowable size. You should now have a screen the same as the screen shot below.

![centos_29.1.PNG](images/00049.jpeg)

Click ok which will return you to your screen showing you your hard drives and all the partitions.

![centos_30.PNG](images/00050.jpeg)

You have now created all the partitions that are required. Click next to continue that partition creation.

![centos_31.PNG](images/00051.jpeg)

Confirm the write changes to disk which will format the hard drive and create the new partitions and file system

Next you will be asked to confirm the boot loader. This will already be pre filled out like the screen shot below so you can just click next.

![centos_32.PNG](images/00052.jpeg)

You will now be on the screen like below with the option of select the software that you wish to install on your server. This has now taken you back to the standard installation of CentOS and you can continue with you installation.

![centos_18.png](images/00053.jpeg)

## Configuring Internet Access

CentOS should now be successfully installed on your server. In order to make your server accessible from the outside would we need to assign it a static ip address. To do this we use the server Ethernet port (LAN) mac address.

Your BT hub that is used as a gateway will now have detected your new server and given it the name of the ports Mac address. First we need to know your servers Mac address that the port is using.

If you only have one server connected then this would not be a problem, but when you come to have multiple servers connected it can get a little confusing.

First you will need to login to CentOS, at present you cannot use SSH to connect so it will have to be via keyboard, mouse and monitor.

![config_1.PNG](images/00054.jpeg)

When CentOS first boots up you will be presented with a screen the same as the screen shot above.

The first two lines tell you your CentOS version and release plus the Kernel. The next line is server1 login:  server1 is the name we assigned the server, server1.example.com.

You will need to login with the username root and press enter. Next will be password. Type your password and press enter. When you type in your password you won’t see any characters displayed, don’t worry this is normal.

Once you have logged in you will see a screen like the shot below.

![config_3.PNG](images/00055.jpeg)

Now that we are logged in we need to get the servers eth0 Mac address so that we can assign the static IP address in the gateway hub.

Enter the following command at the command line prompt and press enter

ifconfig  

This will now present you with the network connections settings. At this time it’s only the first line we are concerned with. In our example screen shot below the line reads: -

eth0   link encap:Ethernet  HWaddr 08:00:27:57:70:B0

![config_4.PNG](images/00056.jpeg)

HWaddr stands for hardware address, the following numbers and letters after this is our Mac address for that eth0 (Ethernet lan port).

We can now login to our gateway hub and assign a static ip address to server.

To access the hub open a browser and type 192.168.1.254 in the browser URL address bar. This is the gateway hub that we configured in configuration of hub 1\. Connection can be done from your personal computer that is connected to the wireless hub 2; as hub 2 connects to hub 1 so this makes both accessible via wireless connections for admin purposes.

Click on settings in the navigation menu and this will prompt you to login. Login with the password you created when configuring your gateway (Hub 1).

Once you have logged in you will need to click on advanced settings from the sub navigation menu and click the button continue to advanced settings.

Navigate to business network – devices

Once the page has loaded you will see a list of all your devices that are connected to your gateway hub. Each device will be listed as below.

![config_5.PNG](images/00057.jpeg)

This is our new server. The gateway hub cannot get the device name so it is listed as unknown and then the mac address. This means we have the right device and the server is connected to the gateway hub. Click on the device to open a new page so that we can configure the settings.

You may want to name this device to something more suitable. In order to rename the device this is done at the first section of the page.

![config_7.PNG](images/00058.jpeg)

In the text field you can enter a preferred name for the device.

Next is assigning the static IP address. In order to do this scroll down the page until you come to the section, Addressing.

![config_6.PNG](images/00059.jpeg)

Once you have found the section in the above screen shot select yes to use public fixed IP address (BT Static IP Service). Select yes to always use this IP address and then from the drop down menu select the IP address you wish to use.

Click on apply and your settings will be saved. The page sometimes takes a little time to refresh but when it does you will see a message like below.

![config_9.PNG](images/00060.jpeg)

Click the ok button. You can now exit and close the gateway hub.

Now that the static IP address has been assigned to the server we need to return to the server for a few last checks.

At the command line enter the following:

system-config-network  

This will open up the network configuration window. The screen shot below is what you should now see.

![config_8.PNG](images/00061.jpeg)

Use you arrow keys to highlight Device configuration and press enter.

You will now see eth0 and the make of your Ethernet controller. If you have more than one Ethernet controller you will see them listed here. We will cover more on multiple IP address later on. Once you have highlighted your Ethernet controller press enter.

![config-10.PNG](images/00062.jpeg)

You will now see a screen like the screen shot below.

![config-11.PNG](images/00063.jpeg)

You will now need to add the primary DNS Server and Secondary DNS Server. To do this use your arrow keys to bring the cursor to the correct field entry. For the Primary DNS Server enter 8.8.8.8 and for the Secondary DNS Server, enter 8.8.4.4 which will now give you a screen like below.

![config-12.PNG](images/00064.jpeg)

Use your arrow keys to highlight the OK tab and press enter which will bring you back to select your device screen. Use your arrow keys to highlight the save tab and press enter.

You will now be returned to the below screen.

![config-13.PNG](images/00065.jpeg)

We now need to edit your DNS configuration file. To do this use your arrow keys to highlight DNS configuration and press enter.

You will now see a screen the same as the screen shot below.

![config-14.PNG](images/00066.jpeg)

The hostname field entry should be left as it is, this is the server hostname that we assigned when installing CentOS. The remaining fields we need to enter.

Use your arrow keys to highlight each of the fields to edit. First edit the Primary DNS to 8.8.8.8 and the Secondary DNS to 8.8.4.4 so they match what we entered in the previous step configuring your Ethernet adaptor. You can leave Tertiary DNS black and delete any information that is in DNS search path.

You will now have a screen like below.

![config-15.PNG](images/00067.jpeg)

Use your arrow keys to highlight the ok tab and press enter which will bring you back to select action screen. Highlight save & quit and press enter.

We now need to restart our server for the settings to take effect. Enter the following command at the command line prompt and press enter

 shutdown –r now  

Your server will now reboot. Once your server reboots, you will be prompted to log back in. Once you have logged back in you will need to enter the following command.

ifconfig  

This will now present you with your network connection settings and will now reflect your static IP address which has been assigned to your server.

Your server is now accessible from the outside world and can now become a headless machine. This means that you can now use putty or any other SSH client to access and configure your web server. To test this you can use your personal computer.

To do this we will need to use software such as putty which is a free telnt/ssh client.

Please see our software chapter for the download location

Once you have downloaded putty you will not need to install anything as this is a standalone software client. Double click on the putty icon which will be in your downloads folder to open a new session. (Example below)

![putty.PNG](images/00068.jpeg)

Once putty is opened the cursor will be blinking in a box called Host Name (or IP address) in this box you need to enter the IP address of your server. When you have entered your IP address click the open button at the bottom.

As this is the first time that you have used putty to connect to your server you will see the following message.

![config-16.PNG](images/00069.jpeg)

There is no need to worry we know that the server is the computer we think it is so you can just click yes to confirm this action.

You will need to login as the root user (root) and the password you created when installing CentOS.

Once the server has confirmed your username and password you will be logged in. As you are connecting to your server via IP address from another computer over the internet this means that your server is now configured ready for internet access.

To exit your SSH client type the following command and press enter.

exit  

Congratulations have now built your first basic web server. If you intend to use cPanel on your web server there are a few more configurations that need to be done before installing cPanel. Please see chapter 7 for this.

# Chapter six

| In this chapter we will cover how to build our Dedicated server, our virtual private server (VPS), create a virtual private server and have our virtual machine auto start on the host start-up. This chapter will also cover installing the host operating system, the virtualisation software and booting CentOS from a saved Image file |

## Building a dedicated server

Building a dedicated server is much easier than virtual servers (VPS) and you can turn an old PC into a dedicated server within an hour.

As we covered previously in this book about selecting hardware and using an old PC for your server you should now have in mind which option you are going to use.

Once you computer is built and tested that all the hardware works correctly and powers up your almost done when it comes to a dedicated server. As a dedicated server uses all the hardware’s abilities all that’s left to do is install CentOS.

You will need to read that chapters on creating a CentOS DVD Rom or a CentOS bootable USB drive and then follow the chapter for installing CentOS.

## Building Virtual Private Server

Virtual private servers are like a computer inside a computer. To do this they use virtualisation software on a host operating system to assign a percentage of the overall system to each virtual machine created.

When deciding on your hardware requirements for the overall host system you will need to consider what each virtual machine will require and what the host will require.

For the example in this book we will allow for two VPS (virtual machines) and one host. Each of the virtual machines will be assigned the following.

*   1 cpu’s
*   1 GB memory
*   20 GB hard disc space

Our host operating system will be windows 8 64 bit and the minimum requirements for this are.

*   1 cpu
*   2 GB memory
*   20 GB hard disc space

So for the total hardware requirements we will need

*   3 cpu’s
*   4 GB memory
*   60 GB hard disc space

It would be good practise to have slightly more than the minimum in case one of the virtual machines needs to be upgraded or another machine needs to be created. I have opted for a 4 core CPU, 4 GB memory and a 500 GB hard drive.

Once the hardware has all been installed and tested that it boots and all the hardware powers up without any problems it is time to create the host system.

### Installing the host operating system

The host operating system is the main control system. They are many different setups that can be created such as a CentOS system which can then be accessed from the outside world to control your virtualisation software but I have opted to use a Windows operating system for this example as most people are comfortable with windows and will find it slightly easier to manage.

If you have a system with windows already installed you can skip this step and continue reading at disabling sleep mode for windows 8.

You do not have to use Windows 8 I have just chosen this for the examples. Windows XP and above work perfectly well as the host operating system; I would recommend a 64 bit operation system version as opposed to a 32 bit.

This installation guide covers both installing Windows 8 from DVD Rom media or Bootable USB drive. Once you have decided how you will install your Host Operating system and created your bootable media you will need to enter your systems bios and select the boot device. This will normally be an option on your computers start up screen when you turn it on.

After your computer loads and selects the bootable media you will be presented with the following screen. This did hang for a good few minutes while the windows setup initialised.

![windows-1.jpg](images/00070.jpeg)

After a few minutes, you will see the Windows Setup screen shown in the screenshot below. This is where you will specify your language settings before clicking next. When you do click next the setup will perform some more initialisation tasks in the background.

I preferred the Windows 8 installation as it was very fast and very easy to install. Most drivers are already installed during installation so very little is left to do or configure.

Windows 8 will install a basic graphics driver and your LAN driver. Your LAN driver is for your Ethernet controller. The one thing that was not installed was the sound driver. This is not a problem as we are using this as a host operating system for the server and sound and fancy graphics are not required.

![windows-2.jpg](images/00071.jpeg)

Once you have completed the above steps and clicked next you will be prompted to install Windows 8 with a screen below.

![windows-4.jpg](images/00072.jpeg)

Once you click the Install now button, you will see the beginning of the information collection phase of the installation procedure. The first step is to enter the Windows 8 product key.

![windows-3.jpg](images/00073.jpeg)

The next step is the Microsoft Licence agreement. You have to accept the agreement if you want to continue with the installation of your Windows 8.

![windows-5.jpg](images/00074.jpeg)

When you are prompted to choose which type of installation you want to perform, as shown in  the below screen shot, you will need to choose Custom: Install Windows only (advanced) type in order to perform a clean installation of Windows 8.

![windows-6.jpg](images/00075.jpeg)

When you are prompted to choose where you want to install Windows, as shown in the screenshot below, you will see a list of any hard drives or partitions that have been created.

There are a number of different options but for the example I will be using the whole drive to install Windows 8 on. For people with experience in creating partitions and installing operating systems you may wish to create your own custom layout.

Options for creating the drive layout could be that you wish to install Windows 8 on a 30 GB partition; this would give you the minimum amount of 20 GB for windows 8 and then the remaining amount of space for the virtualisation software and the CentOS ISO file.

The remainder of the hard drive could then be formatted as say the X drive and used for the virtual machine hard drives. This would give the ability of re-installing windows and your virtualisation software quickly if that part of the drive became corrupt. All you would need to do would be to load your virtual machines back into the virtualisation software and allowing your servers to be back up and running quickly.

![window-7.PNG](images/00076.jpeg)

After you have selected your hard drive layout and you click next, the setup creates any of the hard drive partitions, or the whole drive, formats it, and then instantly moves into the Installing Windows 8 phase which begins with copying and getting files ready for the installation; as shown in the screenshot below. This process can take a short while.

If you do wish to create or delete partitions on the selected hard drive you can do this by clicking on the Drive options (advanced) like which is shown on the bottom right of the above screenshot.

Once these options are loaded you will be presented with the different options for configuring your hard drive.

![windows-8.jpg](images/00077.jpeg)

When Windows has finished installing your screen will change to the screenshot below informing you that Windows needs to restart.

![windows-9.jpg](images/00078.jpeg)

After restarting you will see the black screen with the blue Windows logo and see that setup is getting devices ready, as shown in the below screenshot.

![windows-10.jpg](images/00079.jpeg)

As soon as that part of the process is complete, Windows will alert you that it is going to restart again.

![windows-11.jpg](images/00080.jpeg)

When your system restarts again you will be prompted to choose a colour scheme for Windows 8 and a PC name, as shown below.

![windows-12.jpg](images/00081.jpeg)

When the Settings screen appears, you can choose to customize these settings or you can allow Windows to use the express settings. If you are unsure, you can click the Learn more link and get more details. I chose to use the express settings, you can change any or all of these setting later if you want.

![windows-13.jpg](images/00082.jpeg)

On the next screen you will be prompted to enter how you want to sign into your PC. Windows 8 is designed to work with your hotmail account and load emails direct to your PC from hotmail.

In this step you will just leave this blank. You do not want your host system to have access to your emails and you do not want your host system to require a sign in.

The reason why you do not want your host system to require a sign in is that if your system crashes and causes an automatic restart you would not know about this and until you came to sign back in all your VPS (virtual machines) would be offline.

![windows-14.jpg](images/00083.jpeg)

Next you will see a green screen as shown in the below screenshot indicating that Windows is getting your PC ready. This will take a few minutes and then continue.

![windows-15.jpg](images/00084.jpeg)

The last part of the installation is the apps. Some of you may know that Windows 8 comes with a host of apps on the start screen. These apps are now being installed by default. As this is going to be a host system only, you may want to remove some of these apps or make sure things are not running to create as low a usage footprint as you can, this will allow for more of the systems usage to be put towards your virtual machines.

![windows-16.jpg](images/00085.jpeg)

Once these apps are installed your new Windows 8 installation is complete.

![windows-17.jpg](images/00086.jpeg)

Your Windows 8 host operating system is now installed. There is only one configuration option for Windows 8 as the host operating system that is required which is covered next.

### Disabling sleep mode for Windows 8

By default Windows 8, like most other Windows operating systems sends the PC to sleep after a period of inactivity from the keyboard or mouse. Once our virtual machines have been created this will be a headless machine, meaning we will have no monitor keyboard or mouse permanently active.

If the host operating system was to send the system to sleep we would need to come back to our system and wake it up to allow are servers to be online 24 hours a day. So disabling sleep mode is a necessity.

In order to load the power options menu move the mouse pointer to the bottom left hand of the start screen and right click, and then select power options like the screenshot below.

![windows-18.jpg](images/00087.jpeg)

Once the power options loads you will see, balanced (recommended) highlighted bold and selected. To the right of this is, change plan settings in blue.

![window-19.PNG](images/00088.jpeg)

Once you have clicked on change plan settings the following screenshot loads.

![window-20.PNG](images/00089.jpeg)

Change the ‘put computer to sleep’ select box to never and click save changes. Your host system will not enter sleep mode now after a period of inactivity.

### Installing Virtualisation software

There are various virtualisations software applications available but the one that we are going to use is Oracle’s Virtualbox. This is an open source application and kept well up to date. I have used this for some time and found it to be very easy to use yet very robust for the advanced user.

Please see our software section for the download location.

We are going to be using the 64 bit version of Virtualbox for windows hosts. The current (at the time of this book) is version 4.2.12 the full name of the version that we are going to use is VirtualBox 4.2.12 for Windows hosts x86/amd64.

Oracle has a very good manual and there is plenty of support via forums on using Virtualbox for anybody wishing to explore in more depth the full potential of the software application.

Once you have download Virtualbox you will need to double the application to start the installation process.

As the executable application starts you will see a security warning for your windows system as shown.

![oracle-1.PNG](images/00090.jpeg)

Click Run to start the installation. The Oracle VirtualBox welcome box will now be displayed as shown in the screenshot below. Click Next to begin.

![oracle-2.PNG](images/00091.jpeg)

Next is custom setup. You can just leave this set to its default values for the installation that we require.

![oracle-3.PNG](images/00092.jpeg)

Click next on the above screen. Next you will be prompted if you require the installation to create a desktop shortcut and a shortcut on the quick launch bar. Select or deselect which of these you require and click next.

![oracle-4.PNG](images/00093.jpeg)

On the next screen you will get a warning message. Like the example shot below. This is ok and Virtualbox needs to install network capabilities into your network LAN card and windows configuration files.

Click yes to proceed with the installation.

![oracle-5.PNG](images/00094.jpeg)

The last screen of before Virtualbox is installed is a final conformation and a last chance to change any of the installation settings. Click Install to continue.

![oracle-6.PNG](images/00095.jpeg)

Oracles Virtualbox will now install on your host system. This does only take a few seconds to install. Your installation screen will look like the example screenshot below.

![oracle-7.PNG](images/00096.jpeg)

Just before the installation completes you may get a Windows Security warning message like below. It is ok to check the box Always trust software from “Oracle Corporation” and click install.

![oracle-8.PNG](images/00097.jpeg)

Your installation will now continue and complete in a few seconds which will present you with a completed installation screen like below.

![oracle-9.PNG](images/00098.jpeg)

Uncheck the check box to start Oracle VM VirtualBox 4.2.12 after installation and click finish.

You will now be prompted with a box to restart your system. Click yes and allow your system to restart.

![oracle-10.PNG](images/00099.jpeg)

Windows 8 does seem to configure the network interface into bridge mode very well but other versions of Windows require some manual configuration of for the bridged adapter. This is what allows virtualisation of your network card.

Once your system has rebooted we will now check to make sure that you have the correct network settings to allow Virtualbox to use virtualisation of your network adapter.

In order to via your network settings you will need to go to:

Control panel / network and internet / view network status and tasks

Once the control panel has opened click change adapter settings from the left hand side menu. This will open a new window showing you your Ethernet adapter and your Oracle adapter as in the example screenshot below.

![oracle-11.PNG](images/00100.jpeg)

Once you have the above screen you can right click on VirtualBox Host-Only Network and click disable. You will now see this adapter fade out.

Right click on the Ethernet network adapter and select properties. This will show a small popup box with a list of devices and a check box to the left hand side of each like the example below.

![oracle-12.PNG](images/00101.jpeg)

In our example VirtualBox Bridged Networking driver is the second on the list, make sure this is checked and click ok. This now allows VirtualBox to use your systems built in Ethernet controller and allows virtualisation of the controller so that each of your VPS (virtual machines) can have an independent mac address and internet access.

You should now see a screen like below.

![oracle-13.PNG](images/00102.jpeg)

VirtualBox is now installed and networking is configured ready for you to create you first VPS (Virtual Machine).

### Creating a Virtual Machine (VPS)

Now that we have our host system setup, and our virtualisation software installed, it’s time to create our first VPS (Virtual machine). There really are only a few simple steps to setting the hardware for the machine then it’s just a case of installing and configuring CentOS so that the virtual machine becomes a virtual private server.

If you allowed Oracles VirtualBox to create a desktop icon double click on the Oracle VM VirtualBox icon on your desktop to launch the VirtualBox manager.

As this is the first time the application has been loaded there are no virtual machines created so the default welcome screen is loaded as shown below.

![vps-1.PNG](images/00103.jpeg)

Click on the new tab which is in the top left hand corner of the VirtualBox Manager application. This will launch the create VirtualBox part of the program.

![vps-2.PNG](images/00104.jpeg)

The above screenshot is where we name the machine and operating system. As we are creating a VPS, I have named the machine VPS-1\. In this example we will install CentOS so I have selected the type as Linux, under version CentOS is not listed so I have opted for Other Linux. Once you have selected your options click next.

On the next screen is where you select the amount of memory that the virtual machine should be allocated. You can use the slider but I find it better to type the amount of memory into the text box.

As I mentioned previously that I was going to create two VPS (Virtual machines) each with 1 processor, 1 GB memory and 20 GB hard drive I will need to enter 1 GB in this step. The memory should be entered in MB so I will enter 1024 which is equal to 1 GB.

![vps-3.PNG](images/00105.jpeg)

Next we are prompted to select one of three options. To create a new machine we need to select Create a virtual hard drive now and the click create.

![vps-4.PNG](images/00106.jpeg)

Next we select the type of hard drive we would like to create. VirtualBox can create and use various types of hard drive which are compatible with other virtualisation software applications. As we are only going to use VirtualBox we can leave this setting as the Default as shown in the screenshot below.

![vps-5.PNG](images/00107.jpeg)

On the next screen select fixed size and click next. As shown below.

![vps-6.PNG](images/00108.jpeg)

Now we need to select the hard drive file location and the hard drive size. You can leave the first entry field as it is, if you are happy to use the default location. If you would like to rename the hard drive and select a different file location you can do so here.

The slider scale is for you to increase or decrease the hard drive size. In this example we are creating a 20 GB hard drive; again I just entered this into the text box rather than use the slider.

![vps-7.PNG](images/00109.jpeg)

The VirtualBox Manager will now create your hard drive and set your new machine up. Depending on the size of the hard drive you are creating, will depend on how long this will take.

![vps-8.PNG](images/00110.jpeg)

Once your new virtual machine has been created, you will be returned to the welcome screen of the VirtualBox Manager. This screen will now have changed, and will list your machines on the left hand side with an overview of the machine in the centre of the selected machine; as shown in the screenshot below.

![vps-9.PNG](images/00111.jpeg)

As you can see your new machine is powered off, before we turn your new machine on we need to do a little configuration in order to get the machine to work as a web server.

In order to configure your new machine you will need to make sure that you have your machine selected and highlighted from the left hand menu and click settings, (second tab in on the top menu). Depending on your host system you may get an error warning like below. Don’t worry and click ok.

![vps-10.PNG](images/00112.jpeg)

Now we will have loaded the configuration area for the selected virtual machine which will look like the example screenshot below.

![vps-11.PNG](images/00113.jpeg)

Click on system from the menu on the left hand side.

![vps-12.PNG](images/00114.jpeg)

First we need to change the boot order; we will not be using floppy in our boot order so this can be unchecked. Next highlight Hard Disk, make sure it is checked and use the arrow next to boot order to bring Hard Disk to the top. Now, below hard Disk bring CD/DVD-ROM up to make that as the second boot device and make sure this again is checked.

If you want your server to have more than one processor then you can change this by selecting the Processor tab. Once this opens you can use the slider, or the text input box to increase the processor CPU’s availability for the server. I have left this as 1 CPU for the example.

![vps-13.PNG](images/00115.jpeg)

Windows 8 may not have installed your audio drivers. This is not a problem as we are creating servers, which do not require audio. If you have not got the audio driver installed, it will be better to disable audio on the server so that each time VirtualBox Manager loads and your server boots up you do not get a warning message about this.

Select Audio from the menu on the left hand side, when the page loads uncheck the check box named enable audio, to disable the audio on the server.

![vps-14.PNG](images/00116.jpeg)

Next we need to configure the networking so that the server has an internet connection. Select network from the menu on the left hand side which will load the page as shown below.

![vps-15.PNG](images/00117.jpeg)

Once the page loads you will see a list of adapters numbered 1 -4\. These are your Ethernet ports; which each server has. You can have a maximum of four per server which means you can assign a maximum of four static IP addresses to each of your servers.

With adapter 1 selected click the advanced tab in the centre of the screen. This will load a few more fields of information. Make sure that Enable Network Adapter is checked, next underneath you will find a select box which is named Attached to: use the select box and select Bridged Adapter.

Underneath that you will then see the name of your network adapter. This means that the one Ethernet port on your host system has been virtualised and all adapters access the internet via that one Ethernet port.

As the BT hub can only assign static IP addresses to a dedicated Mac address, and each Ethernet port has one Mac address, then the virtualisation software will assign a slightly different Mac address to each adapter; in effect, creating a virtual Mac address from the hosts’ single Ethernet port.

It might be worth making a note of the Mac address that has been assigned for later when we shall be assigning the IP address.

![vps-16.PNG](images/00118.jpeg)

Click ok to save the settings and return to the main Manager screen.

Your Virtual Machine has almost been made into your VPS. There are just a few more steps to take before we are ready to turn your machine on, and install the server software.

### Installing CentOS 6.3 from a Saved Image

If you have built your host system without a DVD-ROM drive and booted your host system for a USB drive then at the moment you have no way of installing the CentOS server operating system onto your new virtual machine.

Oracles VirtualBox has the added feature of being able to install the operating system directly from a saved image file. This is the ISO file that was downloaded before you created you bootable media.

With a USB Pen drive you can copy the CentOS-6.3-x86_64-bin-DVD1 ISO file from the computer you downloaded it from and save it to your host systems desktop.

Once you have saved your CentOS ISO file to your desktop you can select your new virtual machine to install the operating system from that.

Open your VirtualBox manager page, select your server from the left hand menu and click the settings tab at the top.

When the settings menu loads you will need to select storage from the left hand side menu to load the hard drive screen. On this screen you will see your storage tree and then two devices in that tree.

The first is your virtual machines hard drive which was created when building your virtual machine. In this example mine is called VPS-1.vdi, under that I have a device called Empty. Highlight this device which will change the attributes section to the right.

Under the attributes settings you will see CD/DVD Drive: and this should be listed as IDE Secondary Master in the select box. To the right of that select box you will see a small disc.  Click on the disc and a small menu will open, click on Choose a CD/DVD disc file.

A browse window will open that allows you to browse your computer to find where you have stored your CentOS ISO file. When you have selected your file you will see the attributes section change and the device name change from Empty to your ISO file name.

Click ok to save and exit.

![vps-17.PNG](images/00119.jpeg)

Your virtual machine is now ready to have your CentOS server operating system installed.

When you have returned to your Virtual manager Window select your server and then click start.

When you turn on your machine you will see a few small message windows that appear and until you accept these your machine will not boot. It’s worth taking a note of these messages as we need to select the checkbox not to show this message again or we won’t be able to use the auto boot feature in case you host system crashes and re-boots.

![vps-18.PNG](images/00120.jpeg)

Your machine will now start to load. As we have selected the first boot device to be the hard drive your machine will check the hard drive to boot the operating system. When it detects that there is no operating system installed on the hard drive it will check the CD/DVD ROM drive.

As you have no CD/DVD ROM drive installed that is why we configured the virtual manager settings for this machine to treat the ISO file as the CD/DVD ROM drive.

While your machine is detecting these the screen will look like the screenshot below. This does only take a few seconds.

It’s worth making a note that if you want to select a boot device press F12 this is shown in the bottom of the screen like in the example screenshot below.

Right now you don’t need to know this but for future reference if you have an operating system installed and you want to re-format the server pressing F12 will allow you to select the boot device as a one of event. From there you would select boot from CD/DVD ROM drive.

![vps-19.PNG](images/00121.jpeg)

The screen will change automatically to the beginning of installing CentOS. For instructions on installing CentOS please see the chapter on installing CentOS from a CD/DVD ROM drive.

### Auto start VPS on server boot up

Now that we have our host system built, our virtualisation software installed, and our first server built, we need to allow our server to auto start if the host system is ever re-started.

In order to do this it is really simple on a Windows operating system. Windows has a folder which it checks each time Windows first loads, this folder is called Startup. In some versions of windows the Startup folder can be located differently and be in a different location.

On Windows 8 you can access the Startup folder by using the run command.

From the start screen on Windows 8 type run. (This is the screen where all your apps are shown).

![windows-17.jpg](images/00122.jpeg)

When the run window opens type in the following command

%AppData%

![vps-20.PNG](images/00123.jpeg)

This will open the roaming folder letting you view the folders located within. You will find the Startup folder in \Microsoft\Windows\Start Menu\Programs

Once you have navigated to the Programs folder double click to open the Startup folder.

You can minimise this folder for the moment as we need to create a file first.

The file that we are going to create is a .bat file. This is a type of file that can run at the systems start up and load installed programs.

To create a .bat file you will need to create a new text document. Right click on your desktop, select new and then Text document. This will place a new text document on your desktop. Rename this to something more appropriate. I have called mine onLoad.

Open your new text document and here you will enter the commands that will start your new virtual machine.

There are only two lines of code to enter and these are listed below. The first line is cd, which is the open folder command and then the full location to where you have installed Oracles VirtualBox, (if you have installed VirtualBox in the default location yours will be the same as mine. But it is worth double checking).

The second line is the command to start the VirtualBox manager and start the virtual machine VBox Manage.exe startvm. Then we enter the name of our virtual machine, in this case it is VPS-1.

cd "C:\Program Files\Oracle\VirtualBox\"

VBoxManage.exe startvm "VPS-1"

Now we need to save this text document as a .bat file. Click file and then save as. Enter the File name in the File name field, followed by .bat. In our example we use onLoad.bat, select All Files in the Save as type field and click save.

![vps-21.PNG](images/00124.jpeg)

 ![vps-22.PNG](images/00125.jpeg)

You will now have an icon on your desktop like so:

This is the file that will start your virtual machines each time your host system boots. As you may in the future create more than one virtual machine it would be time consuming going to the Startup folder each time the file needs editing. We can leave the onLoad bat file on the desktop and create a short cut which we can cut and paste into the Startup folder.

Right click on your newly created bat file and select create short cut. The short cut will now be created and saved on your desktop.

Cut and paste this short cut to your Startup folder. You can now close all open windows and restart your host system. When your host system re-boots your virtual machine will auto start.

When your host system boots you will see a command box open like the example screenshot below, then your virtual machine or machines will start.

![vps-23.PNG](images/00126.jpeg)

If you have more than one virtual machine required to start on system boot just add a third line with the name of that machine. Like so: -

VBoxManage.exe startvm "VPS-2"

# Chapter seven

| In this chapter we will cover configuring CentOS ready for CPanel and adding additional IP addresses to your server. |

## Configuring CentOS

CentOS requires a few little configurations prior to installing cPanel. These are all relatively simple and should take no longer than 15 minutes to complete.

cPanel comes with webmail installed which, if your are installing cPanel you will most likely be using the webmail that’s packaged with it. The CentOS installation that we created has postfix installed and running. When postfix is installed and running it conflicts with webmail, so we need to disable and remove this.

cPanel have said they are addressing the issue of stopping and removing postfix as part of the cPanel installation but just to be safe we will stop and remove it first.

In order to perform the configurations required you will need to login to your server. Open your SSH client and login to your server with the IP address, username and password that was created during the CentOS installation and network configuration.

Once you have logged in you will need to run the following two commands pressing enter after each command.

 service postfix stop  

  rpm –e postfix  

Postfix has now been stopped and removed from your server.

Next we need to deactivate the default CentOS firewall. Again this is just two commands to enter.

 chkconfig iptables off  

  service iptables stop  

Next we need to disable SELinux security features.  To do this we need to edit the config file.

To open and edit the config file you will need to type the following command: -

vi  /etc/selinux/config  

To start editing the config file press the (i) key on your keyboard to start the insert mode of the text editor. Use the arrow keys to go to line 6, this should read SELINUX=enforcing, you need to change this to disabled. Once you have changed this you will need to save and exit the text editor.

Press the esc key on your keyboard.

Press the (:) key on your keyboard and then the (w) key, this will now save the config file.

Press the (:) key on your keyboard and then the (q) key, this will quit the text editor and return to command line prompt.

To confirm that the changes have been made you can view the config file again by entering the following command.

vi  /etc/selinux/config  

After editing the config file you should have a file that resembles the following: -

# This file controls the state of SELinux on the system.

# SELINUX= can take one of these three values:

# enforcing - SELinux security policy is enforced.

# permissive - SELinux prints warnings instead of enforcing.

# disabled - No SELinux policy is loaded.

SELINUX=disabled

# SELINUXTYPE= can take one of these two values:

# targeted - Only targeted network daemons are protected.

# strict - Full SELinux protection.

SELINUXTYPE=targeted

Now we need to remove a few of the unwanted yum groups. With the installation of CentOS we have done, these are the following yum groups that we need to remove: -

*   E-mail Server
*   FTP Server
*   KDE Desktop
*   Web Server
*   X Window System

Remember to enter each one with the capitals and lower case letters as they are shown.

To remove these groups enter the following command: -

yum groupremove “E-mail Server”  “FTP Server”  “KDE Desktop”  “Web Server”  “X Window System”  

During the removal you will be asked to confirm with either Y/N. Just enter y for yes, then press enter.

That’s the entire configuration done; we just need to run an update. To do this, enter the following command: -

yum update  

During the update you will be asked to confirm with either Y/N just enter y for yes, then press enter.

Now that all the configuration requirements have been made to CentOS we need to restart our server. To restart the server, enter the following command: -

shutdown  -r now  

## Adding additional IP’s to a VPS

A web server can run with only one IP address, but there are times when more than one IP is required. With our virtualisation software installed on our host system we can have up to four static IP addresses assigned to each of the virtual machines that we create.

The first step is to create the hardware for the IP addresses to be assigned to. Open Oracles VirtualBox manager window and select the virtual machine you wish to add the additional IP addresses to. Make sure the virtual machine is powered off and click settings.

When the setting window opens select network from the left hand side menu, then when that opens select adapter 2 as shown in the screenshot below.

![ip-1.PNG](images/00127.jpeg)

Click the check box next to Enable Network Adapter, this will then turn the second Ethernet adapter on. Next to attached to: we need to select bridge adapter this is to tell the virtualisation software to share the Ethernet controller of or host system.

Click the advanced tab and make a note of the Mac address, you will see that the Mac address of adapter 2 is slightly different to that of adapter 1, although it is sharing the same Ethernet port we have two different Mac addresses that will register in our BT hub and allow us to assign a static IP address to each one.

Power up your server and login using your root username and password created during CentOS installation.

At the command line enter the following: -

system-config-network  

This will open up the network configuration window. The screen shot below is what you should now see.

![config_8.PNG](images/00061.jpeg)

Use your arrow keys to highlight Device configuration and press enter.

Highlight <New Device> and press enter which will open a new window as shown below.

![ip-3.PNG](images/00128.jpeg)

Highlight Ethernet and then click the Add button. For this example we are creating a second Ethernet port so this will be eth1 if you are creating more just increment eth as required.

When the next window opens you will need to fill in the details for the Ethernet port as shown in the example screenshot below.

![ip-4.PNG](images/00129.jpeg)

In the field Use DCHP, it will only have square brackets. The way to insert the asterisk in that field is to highlight the field with the cursor and then use the space button on your keyboard.

When you have finished click the ok button, you will now see your new Ethernet adapter in your Ethernet adapter list. Click the save button to save the changes.

![ip-5.PNG](images/00130.jpeg)

When you are returned to the below screen click save and quit.

![config-13.PNG](images/00131.jpeg)

You will now be returned back to the command line prompt. Before the new settings will take effect you will need to restart your server. Enter the following command: -

  shutdown –r now  

When your server re-boots and you have logged back in enter the following command: -

  Ifconfig   

You will now see eth0 and all its associated settings and also eth1 and its associated settings.

Next you will need to repeat the steps to assign the static IP address in the BT hub. (This was covered in the chapter configuring internet access on page 67). Once you have assigned the static IP address you will need to restart your server for the static IP address to take effect.

## Adding additional IP’s to a dedicated server

Adding additional IP addresses to a dedicated server is very similar to that of a VPS as shown in the examples above. The only difference is how we assign the hardware.

On our dedicated server we don’t have virtualisation software so we need to add a physical Ethernet card. To do this we can add a PCI Ethernet card to one of the PCI ports. These simply slot in with one screw to hold them in place and can be ordered online and delivered for less than £10.

Before adding the Ethernet card you must power off your dedicated server and unplug. When you have done this, remove the side panel and add the PCI Ethernet card to your motherboard.

Power up your server and login using your root username and password.

At the command line enter the following: -

system-config-network  

This will open up the network configuration window. The screen shot below is what you should now see.

![config_8.PNG](images/00061.jpeg)

Use the arrow keys to highlight Device configuration and press enter.

Highlight <New Device> and press enter which will open a new window as shown below.

![ip-3.PNG](images/00132.jpeg)

Highlight Ethernet and then click the Add button. For this example we are creating a second Ethernet port so this will be eth1 if you are creating more just increment eth as required.

When the next window opens you will need to fill in the details for the Ethernet port as shown in the example screenshot below.

![ip-4.PNG](images/00133.jpeg)

In the field Use DCHP, it will only have square brackets. The way to insert the asterisk in that field is to highlight the field with the cursor and then use the space button on your keyboard.

When you have finished click the ok button. You will now see your new Ethernet adapter in your Ethernet adapter list. Click the save button to save the changes.

![ip-5.PNG](images/00134.jpeg)

When you are returned to the below screen click save and quit.

![config-13.PNG](images/00135.jpeg)

You will now be returned back to the command line prompt. Before the new settings will take effect you will need to restart your server. Enter the following command: -

 shutdown –r now  

When your server re-boots and you have logged back in enter the following command: -

  Ifconfig   

You will now see eth0 and all its associated settings and also eth1 and its associated settings.

Next you will need to repeat the steps to assign the static IP address in the BT hub. (This was covered in the chapter configuring internet access on page 67). Once you have assigned the static IP address you will need to restart your server for the static IP address to take effect.

# Chapter eight

| In this chapter we will cover Installing cPanel, PHP, apache and MySQL through to configuring cPanel and adding a domain to the server. |

## Installing cPanel

cPanel is a popular management application that runs on many web servers and is highly supported via cPanel forums and support tickets for all users. It is strongly recommended that you install cPanel as this will make administrating and managing your server easier and the end result will be that you have a stable web server which can host many domain names and websites.

cPanel comes with an abundance of web server software installed such as PHP, apache and MySQL. There are many more but these are pretty much everything you will need to create a professional web server.

cPanel is very easy to install with just three very simple lines of code. When you install cPanel you are granted a 15 day free trial but after that you do have to buy a licence.

The licences can be purchased directly from cPanel per year or you can pay monthly from sources such as cPanel Direct [http://www.cpaneldirect.net/](http://www.cpaneldirect.net/)

The cost is roughly £10 for a VPS licence and £26 for a dedicated server licence; these prices are per month also the price varies monthly depending on the currency exchange as payment is in US dollars.

To begin your installation of cPanel & WHM enter the following three commands at the command line prompted: -

 cd  /home  

  wget  -N  http://httpupdate.cpanel.net/latest  

  sh  latest  

cPanel will now start installing on your web server. This can take up to two hours but I find it’s normally completed within the hour.

When the installation of cPanel has finished you will be presented with a screen like the example below.

![cpanel-1.PNG](images/00136.jpeg)

Once you see that cPanel has installed, (like the bottom three lines in the above screenshot) you are now ready to login to cPanel and run the initial setup configuration.

## Configuring cPanel

Now that cPanel has installed on your server it is time to login and confirm a few settings. You will be guided through each of these setting at each step with an explanation on each one step where needed.

It would be too much to put a full explanation of cPanel in this book but cPanel docs are available for you to read online in fantastic easy to follow instructions.

Whilst cPanel is installing take the time to read through the guide at the below link to learn how to cover the 6 steps of the initial setup.

[http://docs.cpanel.net/twiki/bin/view/AllDocumentation/WHMDocs/WHMInitialSetup](http://docs.cpanel.net/twiki/bin/view/AllDocumentation/WHMDocs/WHMInitialSetup)

To access cPanel you will need to type the IP address followed by; :2086 into your web browsers url address bar.

When you access WHM panel you will be asked for your username and password. These are the user name root and password that was created during the CentOS installation.

Under step two of the initial setup you are asked to confirm your resolvers. If you remember back to when we configured CentOS for the internet we entered primary and secondary resolvers; these where 8.8.8.8 and 8.8.4.4, these will be you resolvers for the initial setup and will most probably already be entered.

Under step three of the initial setup is your server IP addresses. Your primary IP address will already be added so no need to add this again.

Follow the instructions for step four carefully. This is the Name servers section. Name servers are where you tell your domain name to point and are for example ns1.example.com and ns2.example.com.

In order to use your own name servers you will need to setup glue records for your domain name. Ask whoever registers your domain name to assign glue records to your domain name for you. You will need to provide them with the IP address of your server, you will need two glue records and both glue records can have the same IP address.

You will then need to ask them to point your domain name to your new name servers.

After you have completed this step you will need to wait about 24 hours for the domain name and name servers to propagate around the internet.

## Adding a domain name

Now that cPanel is installed and the initial setup is completed it is time to start creating a package so that you can assign a domain name to the server; if you have not done so already it is worth browsing the online documentation about cPanel so that you have a basic understanding of where things are and how they function.

Before you can add a domain name to your server you will need to create a package that the domain name can be assigned to. To do this you will need to login into WHM panel.

When you have logged in you will have a links menu on the left hand side of your screen. Scroll down a little over half way until you see the heading packages. Under that click add package which will load the screen like the example screenshot below.

![cpanel-2.PNG](images/00137.jpeg)

First we need to name the package. I am only going to have one website on this test server so I will want it to use the full potential, effectively an unlimited package so I will call this package unlimited.

The next section is resources; this is where you can create custom packages which are limited. This is how shared web hosting accounts are limited, the package is created with limitations and then the domain name assigned to that particular package.

You do not have to create a package for every domain name, you can assign more than one domain name to a package as long as you want each domain name account to have the same limitations.

Under the settings section you can leave these as the defaults like the example screenshot below.

![cpanel-3.PNG](images/00138.jpeg)

Next click add to create and save your new package.

Now that you have created your package we can create a new account on the server and assign the domain name to that account.

Scroll down the links menu on the left hand side until you come to the heading account functions. Click on create a new account which will load the screen like the example screenshot below.

![cpanel-4.PNG](images/00139.jpeg)

The first section is the domain information. This is the domain name that you have registered with your domain name registrar. Fill in the required fields and you should then have that section like the example screenshot below.

The email is the server administrators email address for who will maintain that account.

![cpanel-5.PNG](images/00140.jpeg)

Next we have to assign the account to a package; this is the package we created previously. Select your package from the select box.

![cpanel-6.PNG](images/00141.jpeg)

Next is the settings, these can just be left as the default settings and themes.

![cpanel-7.PNG](images/00142.jpeg)

The next setting can just be left as this is used when you wish to create reseller accounts on the server.

![cpanel-8.PNG](images/00143.jpeg)

We are almost done, now we need to select the DNS settings. Make sure you check the check box that states use the nameservers specified at the domains registrar (ignore locally specified nameserves).

![cpanel-9.PNG](images/00144.jpeg)

The last option is the mail settings. If you want to use webmail that is packaged with the server you can leave this as the local mail exchanger or you can select automatically detect configuration.

![cpanel-10.PNG](images/00145.jpeg)

Finally click the create button and your account will be created and the domain name assigned to the server.

If you have not left your domain name and server for 24 hours since registering your domain name, applying glue records and name servers then you may have to wait still for propagation to accrue.

If it has been almost 24 hours then your domain name and name servers are probably fully active around the internet and you are ready to test that your domain name resolves to your new web server.

Enter your domain name into the URL address bar of your browser. If you get a page loaded like the example screenshot below then your domain name is resolving to your web server correctly and you are ready to create your web pages and upload them to the server.

![cpanel-11.PNG](images/00146.jpeg)

If you don’t see this page then this could just be a DNS propagation issue, you can check this at [http://www.intodns.com/](http://www.intodns.com/)

If you are still having problems you can visit the support website for help, the details are in the technical support chapter. I will be happy to take a look for you.

# Chapter nine

| In this chapter we will cover some basic server security from creating wheel users, disabling root access, changing the SSH port and installing a server firewall. |

## Creating a wheel user and disabling root access

Disabling root access via SSH to your server provides an additional two levels of security. I strongly advise you taking this action as well as changing your SSH port. Servers come under a number of attacks most of which are aimed at gaining access your server.

Once a wheel user is created and root access has been disabled you must login via SSH to your server with a user account that has root privileges and then switch to the root user. This makes the server request two valid logins before full root access is granted.

Wheel users are also known as supper users. In the next few steps I will guide you through, first how to create a wheel user and grand root privileges to that user then secondly, how to disable root access.

Disabling root access via SSH does not disable root username and password login for cPanel and WHM, you will still use the user name root and the password that was created during the CentOS installation. If you do not have a strong password already for the username root I would recommend logging into your WHM panel and changing the root password to a very strong one. Once the password has been changed in the WHM it will change the root password for all other root logins to your server, for example root login via SSH.

The first step is to create the new user, as normally the only person who needs to login to the server is the technical support person I will call this user tecsupport.

Login to your server via SSH with your root username and password. Once you have logged in issue the following two commands: -

  adduser  tecsupport  

  passwd  tecsupport  

You will now see a screen in your SSH client like the example below asking you to enter the new password for the user tecsupport. Pick a password that you can remember,but yet is strong enough not to be guessed.

![wheel-1.PNG](images/00147.jpeg)

Once you have entered the new password you will be asked to confirm the password. After you have confirmed you will see a message stating all authentication tokens updated successfully.

Next we need to add the user tecsupport to the wheel group. To do this we are going to edit a file. At the command line prompt issue the following command: -

  vi  /etc/group   

You will now see your window change to the same as the example screen shot below. We need to enter the insert mode so to do this press the (i) key on your keyboard.

![wheel-2.PNG](images/00148.jpeg)

Using the arrow keys on your keyboard scroll down until you come to the line that reads wheel:x:10: and change this to read wheel:x:10:tecsupport to add the user tecsupport to the wheel group.

Press the esc key on your keyboard.

Press the (:) key on your keyboard and then the (w) key, this will now save the file.

Press the (:) key on your keyboard and then the (q) key, this will quit the text editor and return to command line prompt.

Now that we have added the user we will need to restart sshd in order for the settings to take effect. You will now be back at the command line prompt and you will need to issue the following command: -

  /etc/init.d/sshd  restart   

We have now created the wheel user and granted them root access, next we need to disable root login. To do this we need to edit another file. Issue the following command at the command line prompt: -

 vi  /etc/ssh/sshd_config   

When the fill opens you will only see a small part of the file, use your arrow keys to scroll down until you come across the line that reads #PermitRootLogin yes.

This is the line we need to edit. We need to enter the insert mode so to do this press the (i) key on your keyboard.

Change the line from #PermitRootLogin yes to PermitRootLogin no remembering to remove the hash symbol from the start of the line.

Press the esc key on your keyboard.

Press the (:) key on your keyboard and then the (w) key, this will now save the file.

Press the (:) key on your keyboard and then the (q) key, this will quit the text editor and return to command line prompt.

Now that we have edited the file we will need to restart sshd in order for the settings to take effect. You will now be back at the command line prompt and you will need to issue the following command: -

  /etc/init.d/sshd  restart   

We have now disabled root login. Do not exit you SSH client because if any mistakes have happened you may not be able to log back in as root, the current SSH session is already logged in so keep that open.

Open a new SSH client window and we will login with the Wheel user that we have created.

Now that you have logged in we need to switch to the super user, to do this issue the following command: -

  su   

You will now be asked for a password. This is the root password that is being required.

You can check that you are now acting as root by issuing the following command: -

  whoami   

Your window should look like the example screenshot below and you can see that the line after issuing the command whoami, states you are root.

![wheel-3.PNG](images/00149.jpeg)

You can now close off your SSH windows by issuing the following command. (If you have logged in and switched to the super user you will need to issue the command twice.): -

  exit   

## Changing your SSH port

While there are many ways to make sure your server is as secure as possible there are some basic steps and measures that you can take to cover your bases.

The Secure Shell (SSH) Protocol by default uses port 22\. Accepting this default value does not make your system insecure. Changing the port will not provide a significant variance in security. However, changing the default SSH port will stop many of the automated attacks your server will face and a will make it a bit harder to guess which port SSH is accessible from, in other words, a little security through obscurity.

The easiest way to change the port is to SSH into the server as the root user:

To do this we will need to use software such as putty which is a free telnt/ssh client.

Please see our software chapter for the download location

Once you have downloaded putty you will not need to install anything as this is a standalone software client. Double click on the putty icon which will be in your downloads folder to open a new session. (Example below)

![putty.PNG](images/00068.jpeg)

Once putty is opened the cursor will be blinking in a box called Host Name (or IP address) in this box you need to enter the IP address of your server. When you have entered your IP address click the open button at the bottom.

You will need to login as the root user (root) and the password you created when installing CentOS.

As root, use the text editor (vi) to edit the sshd configuration file. This can be done by typing the following on the command line: -

  vi /etc/ssh/sshd_config  

Next you will need to locate the line that specifies the port. If your sshd_config file has not been altered, the Port setting will be commented out with a # symbol (example below): -

![ssh_2.PNG](images/00150.jpeg)

The # symbol tells the server to ignore anything after it on the same line, so we will need to remove that character and then change the number 22 to something else. Be sure you do not pick a port number that is in use by a different service.

The default line will look like this:

#Port 22

In this example the port has been changed to 2922 and the # symbol removed. (Example below)

![ssh_1.PNG](images/00151.jpeg)

Press the (i) key on your keyboard to start the insert mode of the text editor. Once you have changed your port number and removed the # symbol you will need to save and exit the text editor.

Press the esc key on your keyboard.

Press the (:) key on your keyboard and then the (w) key, this will now save the config file.

Press the (:) key on your keyboard and then the (q) key, this will quit the text editor and return to command line prompt.

Next is to restart SSH in order for the new settings to take effect.

  /etc/init.d/sshd restart   (example below)

![ssh_3.PNG](images/00152.jpeg)

Your SSH service has now been restarted and the new SSH port has taken effect.

## Installing server firewall

To install the server firewall you must be logged in to the server as the root user. I will cover logging and switching to super user for the people who have disabled root access and created a wheel user account.

For people that have not created a wheel user and deleted root access you can skip this step.

Login and switch to super user

You will need to login to the server via SSH and switch to the super user.

Open a new SSH client window and we will login with the Wheel user that you have created.

Now that you have logged in we need to switch to the super user, to do this issue the following command: -

  su   

You will now be asked for a password. This is the root password that is being required.

You can check that you are now acting as root by issuing the following command.

  whoami   

Your window should look like the example screenshot below and you can see the line after issuing the command whoami states you are root.

![wheel-3.PNG](images/00149.jpeg)

We need to be in the main directory folder and at the moment you can see we are in /home/tecsupport, in order to go back you will need to issue the following command: -

cd  ../../  

You will now see that the current directory has changed on the bottom line as shown in the example screenshot below.

![firewall-1.PNG](images/00153.jpeg)

Installing Firewall as root user

Now that you have logged into the server as the root user we can install the firewall on the server. There are four commands to issue in order to download and install the server. The commands are listed below and after each command press the enter key on your keyboard and allow each command to execute before continuing to the next.

wget  http://www.configserver.com/free/csf.tgz  

tar  -xzf  csf.tgz  

cd  /csf  

sh  install.sh  

The output when completed will look like the example screenshot below. You can now logout of your SSH client, if you have switched to the super user you will need to use the exit command twice.

The exit command is: -

exit  

![](images/00154.jpeg)

The firewall will now be installed on your server and is ready to be configured and activated. You will need to login to your servers WHM panel and from the links menu on the left hand side the firewall should be at the very bottom under plugins as shown in the example screenshot below. If plugins and the firewall are not showing in the links menu you will need to logout of the server and log back in.

![firewall-3.PNG](images/00155.jpeg)

When you open the window for your firewall you will see that the firewall is enabled but in test mode, the is at the top of the firewall window as shown in the screenshot below.

![firewall-4.PNG](images/00156.jpeg)

When the firewall is in test mode it allows you to make configuration changes and test the firewall so that any changes you make do not lock you out of your server.

Whenever you go to make changes to your firewall settings you should put your firewall into test mode first.

In order to activate your firewall you must edit the configuration firewall so that it is no longer in test mode. Scroll down until you find the section shown in the screenshot below.

![firewall-5.PNG](images/00157.jpeg)

The button we need is the second button from the top named Firewall Configuration. Once this is clicked your page will refresh and show you your firewall configuration file as shown below.

![firewall-6.PNG](images/00158.jpeg)

After the copyright section the first section of text reads: -

# Testing flag - enables a CRON job that clears iptables incase of
# configuration problems when you start csf. This should be enabled until you
# are sure that the firewall works - i.e. incase you get locked out of your
# server! Then do remember to set it to 0 and restart csf when you're sure
# everything is OK. Stopping csf will remove the line from /etc/crontab
#
# lfd will not start while this is enabled

In the text field below this you will need to enter 0 and then scroll down to the bottom of the page and click the change button. Your page will now refresh and load as shown in the screenshot below.

![firewall-7.PNG](images/00159.jpeg)

Click the Restart csf+lfd button to restart your firewall and activate the new settings. Your page will refresh with a lot of data about flushing, drop and accept, if you scroll down to the bottom of the page you will see text shown in the screenshot below and a return button

![firewall-8.PNG](images/00160.jpeg)

After you have returned to your firewall home page you will see that the status of your firewall has now changed to Enabled and Running.

![firewall-9.PNG](images/00161.jpeg)

You can run a check of your server’s security and any recommendations for firewall settings by clicking on the Check Server Security button. This will perform a basic security, stability and settings check on the server. You can see from the screenshot below that it is the first button in the server security information section.

![firewall-10.PNG](images/00162.jpeg)

This will now run a test on the server and produce an output with ok and warnings. Next to each warning there will be recommendations on settings to change to improve the security on the server.

At the very bottom of the page you will have the overall score of the check. As you can see from the screenshot below that the score is pretty low so a few of the recommended settings will need to be adjusted to improve the server security.

![firewall-11.PNG](images/00163.jpeg)

Do remember to put the firewall back into test mode before making any configuration changes.

# Chapter Ten

| In this chapter we will cover some basic optimising of your server. This will include configuring MySQL for heavily database driven websites, changing full text searching for three letter words. |

## Optimising MySQL

Here we will cover the basics in optimising MySQL for database driven websites. To achieve this we will be editing the my.cnf file and to do this you will need root access via your SSH client; such as putty to access and edit via commend line on your new server.

Configuring MySQL to optimise your server and performance will have a major impact on speed and the hardware of your server, in some cases reducing the server load by almost half.

We will cover the most importantly used variables for MySQL configuration files and a MySQL monitoring solution to allow you to monitor and tweak your MySQL configuration file to meet your servers unique requirements.

All MySQL optimisation settings are stored in your my.cnf file located on your server. By default this file has very little, if anything at all in it by default; this means we will be adding a few lines in order to optimise MySQL.

The reason why there are so few settings in the my.cnf file is that every server environment is different. Each has different server memory, different sites and some servers are running database driven websites and others are not. This means that the configuration files for MySQL are unique to each environment.

The MySQL settings we will use have been broken down in to four categories which are listed below with a short break down for each category. Where we have M & K in our my.cnf settings these stand for Megabytes (M) and Kilobytes (K).

Defaults setting

The only default settings that that maybe in your my.cnf is the max connections. However this is not always present. The default is 100 on older versions of MySQL but this should now have this variable increased to 500\.

The reason why 500 should now considered best number for this variable is that the default max number of connections for Apache is 512\. If this is left at 100 in the my.cnf file and Apache is sending child processes at around 500 then after MySQL has connected 100 the rest will be rejected; MySQL will then start returning errors. It is best to keep these both around the same number.

max_connections = 500

Chache

These are the common variables that I believe should be in all my.cnf files.

The first one is thread_cache_size, the default for this is 0\. The thread cache size is the number of threads the server should cache for reuse. A starting value for this would be 4 and can then be monitored via MySQL tuner for optimal performance.

Next is table_cache the default value for this is 64\. The table cache is the number of open tables for all threads.

Next we have query_cache_limit; the default for this is 1M which means that anything that is to be stored in the query cache cannot be larger than 1M.

Next we have query_cache_size; the default value for this is 0 which means there is no query cache even if it is enabled. A starting value for the query cache size would be 6, the query cache size is the amount of memory for cache and queries which means that the same queries do not have to keep getting pulled from the database and can speed up results.

Next we have query_cache_type; the default for this is 1, 0 means it is off or there is an optional value of 2 which means that it is on if a database needs it.

Buffer

The first one is the key_buffer_size; the default for this is 8M and this is the buffer size for indexed blocks. A good starting value is 24M and can be monitored and amended as needed.

Next we have read_buffer_size; the default value is 128K and this is the tread sequential table scan buffer size.

Next we have the join_buffer_size; the default value is 128K and this is a variable that can be set to speed up joins that do not have indexing.

Others

First we have connect_timeout; this is the number of seconds that MySQL will wait for a packet before it sends a bad request. The default value for this is 10 which stands for 10 seconds, if you have a slow server you can increase this so that users do not see a lot of bad requests because MySQL is timing out.

Next we have max_connect_errors; the default value for this is 10\. This is the maximum number of interrupted connections from a host. The number of interrupted connections would need to run in a row which would result in the host being permanently blocked. To unblock them you would have to run flush hosts in MySQL command line.

Next we have max_allowed_packet; the default size for this is 1M, this is the maximum size of the packet that can connect.

Next we have tmp_table_size; this is the maximum size of the temp table size. This is a system specific setting and a good starting point would be 8M and then any required monitoring and adjusting.

Now that you are ready to edit and optimise your my.cnf file you will need to login to your server via your SSH client such as putty. If you have not used putty or some other SSH client before please see our chapter ‘Changing your SSH port’ for instructions on how to use putty.

Once you have logged in to your server you will need to execute the following command in order to open your my.cnf file ready for editing: -

vi /etc/my.cnf  

Once the MySQL my.cnf file has opened press the (i) button on your keyboard to start the insert mode. Use the arrow keys to move to a new blank line and make sure there is no character at the start of the line such as (  ̴).

Template file

Below is a template file of the contents your my.cnf should have. These are the basic optimisation settings your server should start with. There are a few variables included in the template file and higher values that we mentioned earlier but these variables and values can be monitored and adjusted in MySQL Tuner as and when necessary.

Once these setting have been added to your my.cnf file you will need to restart MySQL and then monitor your MySQL performance.

These default variable settings have been set for a server which is running a heavy load database and you may need to alter and tweak these settings over a few days in order to get the best setting for your server. To do this we will use MySQL Tuner. More about MySQL Tuner is below.

### DEFAULT SETTINGS ###

max_connections = 500

### CACHE ###

thread_cache_size = 1M

table_cache = 64M

query_cache_limit = 4M

query_cache_size = 16M

query_cache_type = 1

### Buffer ###

key_buffer_size = 32M

read_buffer_size = 128K

join_buffer_size = 128K

###OTHERS ###

connect_timeout = 10

max_connect_errors = 10

max_allowed_packet = 1M

tmp_table_size = 16M

max_heap_table_size = 16M

Now that the MySQL variables have been added to the my.cnf you will need to exit the insert mode, save and quit. To do this you will need to execute the following commands: -

Press the esc button on your keyboard. This will exit the insert mode. Next you will need to type the following commands pressing enter after each command: -

:w  

:q  

MySQL will now need to be restarted. In order to restart MySQL you will need to issue the following command: -

/etc/rc.d/init.d/mysql restart  

Whilst editing files at command line you may have an interrupted connection and have to restart your SSH client. If this happens you will receive an error message when you log back in and try to edit a file. For example, if, when editing your my.cnf file and your system crashed you would be asked to recover or remove the swp file. It may be best to remove the swp file and start afresh. In order to remove this file you can issue the following command: -

rm /etc/.my.cnf.swp  

Once you have done this you will be free to continue editing the file.

MySQL Tuner

In order to monitor the MySQL system and make any recommended alterations it will be beneficial to install mysqltuner.pl; this will monitor MySQL and suggest any alterations needed for the my.cnf file. The mysqltuner.pl will need to be installed and MySQL running for a minimum of 24 hours for accurate results to be noted. So, after each alteration to the my.cnf file and MySQL has been restarted do wait at least 24 hours in order for the MySQL Tuner to monitor your MySQL processes and give accurate recommendations.

To install mysqltuner.pl complete the following commands and pressing Enter after each command: -

wget mysqltuner.pl  

chmod 755 mysqltuner.pl  

MySQL Tuner is now installed and running on your server. To run and test your MySQL system software run the following command: -

./mysqltuner.pl  

This will output a display in relation to your MySQL system software and recommend any changes needed for your my.cnf file. Other recommendations such as repair and optimise maybe part of your recommendations. In order to do this you can issue the following commands in the command line prompt: -

 mysqlcheck  - -all-databases -r   = Repair tables and databases

 mysqlcheck  - -all-databases -o   = Optimise tables and databases

## Change full text search min word length

This will allow full text searching to allow words of three characters instead on the standard four.

1.  Login to the server with root access
2.  Make sure you are in the main root directory cd  ../ and then ls
3.  Next is to edit the file.
    *   vi  /etc/my.cnf
    *   add the following line of code ft_min_word_len = 3
    *   Exit the edit mode and save file by pressing the escape tab, then pressing : and typing wq to save the file.
4.  Next is to stop and start mysql

*   /etc/rc.d/init.d/mysql   stop
*   /etc/rc.d/init.d/mysql  start
*   /etc/rc.d/init.d/mysql restart

5.  Next is to repair the mysql database for all accounts on the server

*   mysqlcheck   --all-databases  -r = Repair
*   mysqlcheck  --all-databases -o = optimise

# Chapter Eleven

| This chapter is where to go for further support or with help understanding any part of this book. |

## Technical support

As I have covered so much in this book it is understandable that it may be a little daunting and you may want the reassurance that support is on hand for further questions, advice or if you are struggling with any aspect of the installation and would like this completed for you.

You can always get email support from a professional by visiting the website where we would be more than happy to help.

As software changes from time to time, upgrades and updates happen which may change part of an installation or configuration; so to combat this we will publish any updates on the website that may affect any of the installation aspects of this book.

If you do wish to visit the website for further help or advice please visit us at: -

http://www.buildawebserver.co.uk

# Chapter Twelve

| This chapter will cover all the software we have used in creating our dedicated and virtual private servers. |

## Software

This is a list of all the software we have used during this book to create our dedicated and virtual private servers. You may not need all of this software as I have ran through various configuration options in the book and not all will be applicable to you.

I have tried to use as much open source (Free Software) where possible.

### Winrar

Download location: [http://www.win-rar.com/](http://www.win-rar.com/)

Price:                                          free

### WinZip self extractor

Download location: [http://www.winzip.com/win/en/downse.htm](http://www.winzip.com/win/en/downse.htm)

Price:                                          free

### ISO2USB

Download location: [http://iso2usb.sourceforge.net/](http://iso2usb.sourceforge.net/)

Price:                                          free

### Windows 7 USB/DVD Download Tool

Download location:

[http://www.microsoftstore.com/store/msstore/html/pbPage.Help_Win7_usbdvd_dwnTool](http://www.microsoftstore.com/store/msstore/html/pbPage.Help_Win7_usbdvd_dwnTool)

Price:              free

### CentOS x86 64bit

Download location: [http://isoredirect.CentOS.org/CentOS/6/isos/x86_64/](http://isoredirect.centos.org/centos/6/isos/x86_64/)

Price:                                          Free

### Windows 8 64 bit Bit operating system

Available on eBay

Price:                                          various (average £84.99)

### uTorrent

Download Location: [http://www.utorrent.com/](http://www.utorrent.com/)

Price:                                          free

### Image Burn

Download location: [http://www.imgburn.com/](http://www.imgburn.com/)

Price:                                          free

### Putty: a free Telnet/SSH Client

Download location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/](http://www.chiark.greenend.org.uk/~sgtatham/putty/)

Price:                                          free

### Oracle Virtualbox

Download location: [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)

Price:                                          free

### cPanel

Website: [http://cpanel.net/](http://cpanel.net/)

Price:                                          from £10 - £26 per month