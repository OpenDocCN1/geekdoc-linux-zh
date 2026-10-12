
Table 1-1 (continued)

| Feature | Dial-up | DSL | Cable |
|---|---|---|---|
| Typical speed | 56 Kbps maximum | 640 Kbps download, 128 Kbps upload (higher speeds cost more) | 1.5 Mbps download, 128 Kbps upload |
| One-time costs (estimate) | None | Install = $100-200; Equipment = $200-300 (may be leased and may require activation cost) | Install = $100-200; Equipment = $60-100 (may be leased) |
| Typical monthly cost (2003) | Phone charges = $20/month; ISP charges = $15-30/month | $50/month; may require monthly modem lease | $50/month; may require monthly modem lease |

Note: Costs vary by region and provider. Costs shown are typical ones for U.S. metropolitan areas.

## Connecting with DSL

DSL stands for Digital Subscriber Line. DSL uses your existing phone line to send digital data in addition to the normal analog voice signals (analog means continuously varying, whereas digital data is represented by 1s and 0s). The phone line goes from your home to a central office, where the line connects to the phone company's network — by the way, the connection from your home to the central office is called the local loop. When you sign up for DSL service, the phone company has to hook up your phone line to some special equipment at the central office. That equipment can separate the digital data from voice. From then on, your phone line can carry digital data that can then be directly sent to an Internet connection at the central office.

## How DSL works

A special box called a DSL modem takes care of sending digital data from your PC to the phone company's central office over your phone line. Your PC can connect to the Internet with the same phone line that you use for your normal telephone calls — you can make voice calls even as the line is being used for DSL. Figure 1-1 shows a typical DSL connection to the Internet.

Your PC talks to the DSL modem through an Ethernet connection, which means that you need an Ethernet card in your Red Hat Linux system.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_316_0.png)

Figure 1-1:
DSL provides high-speed connection to Internet over a regular phone line.

Your PC sends digital data over the Ethernet connection to the DSL modem. The DSL modem sends the digital data at different frequencies than those used by the analog voice signals. The voice signals occupy a small portion of all the frequencies that the phone line can carry. DSL uses the higher frequencies to transfer digital data, so both voice and data can travel on the same phone line.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_316_1.png)

The distance between your home and the central office — the loop length — is a factor in DSL's performance. Unfortunately, the phone line can reliably carry the DSL signals over only a limited distance — typically three miles or less. This means that you can get DSL service only if your home (or office) is located within about three miles of your phone company's central office. Your phone company can tell you whether your location can get DSL or not. Often it has a Web site where you can type in your phone number and get a response about DSL availability. For example, try www.dslavailability.com for U.S. locations.

## DSL alphabet soup — ADSL, IDSL, SDSL

I have been using the term DSL as if there were only one kind of DSL. As you may imagine, nothing is ever that simple. There are, in fact, three variants of DSL, each with different features. Take a look:

- **ADSL:** Asymmetric DSL, the most common form of DSL, has much higher download speeds (from the Internet to your PC) than upload speeds (from your PC to the Internet). ADSL can have download speeds of up to 8 Mbps and upload speeds of up to 1 Mbps. ADSL works best when your location is within about 2½ miles (12,000 feet) of your central office. ADSL service is priced according to the download and upload speeds you want. A popular form of ADSL, called G.lite, is specifically designed to work on the same line you use for voice calls. G.lite has a maximum download speed of 1.5 Mbps and maximum upload speed of 512 Kbps.
- **IDSL:** ISDN DSL (ISDN is an older technology called *Integrated Services Digital Network*) is a special type of DSL that works at distances of up to five miles between your phone and the central office. The downside is that IDSL only offers downstream (from the Internet to your PC) and upstream (from your PC to the Internet) speeds of up to 144 Kbps.
- **SDSL:** Symmetric DSL provides the equal download and upload speed of up to 1.5 Mbps. SDSL is priced according to the speed you want, with the higher speeds costing more. The closer your location is to the phone company central office, the faster the connection you can get.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_317_0.png)

DSL speeds are typically specified by two numbers separated by a slash, like this: 1500/384. The numbers refer to data-transfer speeds in kilobits per second (that is, thousands-of-bits per second, abbreviated Kbps). The first number is the download speed, the second the upload. Thus 1500/384 means you can expect to download from the Internet at a maximum rate of 1,500 Kbps (or 1.5 Mbps) and upload to the Internet at 384 Kbps. If your phone line's condition is not perfect, you may not get these maximum rates — both ADSL and SDSL adjust the speeds to suit existing line conditions.

The price of DSL service depends on which variant — ADSL, IDSL, or SDSL — you select. For most home users, the primary choice is ADSL (or, more accurately, the G.lite form of ADSL) with transfer speed ratings of 1500/128.

## Typical DSL setup

To get DSL for your home or business, you have to contact a DSL provider. In addition to your phone company, there are many other DSL providers. No matter who provides the DSL service, some work has to be done at your central office — the place where your phone lines connect to the rest of the phone network. The work involves connecting your phone line to equipment that can work with the DSL modem at your home or office. The central office equipment and the DSL modem at your location can then do whatever magic is needed to send and receive digital data over your phone line.

Because of the need to set up your line at the central office, it takes some time after you place an order to get your line ready for DSL.

The first step for you is to check out the DSL providers that provide service and see if you can actually get the service. Because DSL can work only over certain distances — typically less than 2.5 miles — between your location and the central office, you have to check to see if you are within that distance limit. Contact your phone company to verify. You may be able to check this on the Web. Try typing into Google (www.google.com) the words DSL availability, and your local phone company's name. You probably will get a Web site where you can type in your phone number and learn if DSL is available for your number.

If DSL is available, you can look for the types of service — ADSL versus SDSL — and the pricing. The price depends on the download and upload speeds you want. Sometimes phone companies offer a simple residential DSL (basically the G.lite form of ADSL) with a 1500/128 speed rating — meaning you can download at 1,500 Kbps and upload at 128 Kbps. Of course, these are the maximums, and your mileage may vary.

After selecting the type of DSL service and provider, you can place an order and have the provider install the necessary equipment at your home or office. Figure 1-2 shows a sample connection diagram for typical residential DSL service.

Figure 1-2:
You can connect a PC's Ethernet card directly to the DSL modem.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_318_0.png)

Here are some key points to note in Figure 1-2:

- Connect your DSL modem's data connection to the phone jack on a wall plate.
- Connect the DSL modem's Ethernet connection to the Ethernet card on your PC.
- When you connect other telephones or fax machines on the same phone line, install a *microfilter* between the wall plate and each of these devices.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_319_0.png)

Because the same phone line carries both voice signals and DSL data, you need the microfilters to protect the DSL data from possible interference. You can buy them at electronic stores or from the DSL provider.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_319_1.png)

When you connect your Red Hat Linux PC to the Internet using DSL, the connection is always on — and there is more potential for outsiders to break into the PC. You should make sure that the Red Hat Linux firewall setting is set at High Security. To configure the firewall settings, choose Main Menu→System Settings→Security Level from the GNOME desktop.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_319_2.png)

There is another way to protect your Red Hat Linux system from intruders and, as an added bonus, share the high-speed connection with other PCs in a local area network (LAN). To do this, you need a router that can perform Network Address Translation (NAT). Such a *NAT router* translates multiple private Internet Protocol (IP) addresses from an internal LAN into a single public IP address, which makes it possible for all the internal LAN PCs to access the Internet.

If you also want to set up a local area network, you need an Ethernet hub to connect the other PCs to the network. Figure 1-3 shows a typical setup that connects a LAN to the Internet through a NAT router and a DSL modem.

Here are the points to note when setting up a connection like the one shown in Figure 1-3:

- You need a NAT router with two 10BaseT Ethernet ports (the 10BaseT port looks like a large phone jack, also known as an *RJ-45 jack*). Typically, one Ethernet port is labeled *Internet* (or External or WAN for wide-area network work), and the other one is labeled Local or LAN (for local area network).
- You also need an Ethernet hub. For a small home network, you can buy a 4- or 8-port Ethernet hub. Basically, you want a hub with as many ports as the number of PCs you intend to connect to your local area network.
- Connect the Ethernet port of the DSL modem to the Internet port of the NAT router, using a 10BaseT Ethernet cable (these look like phone wires with bigger RJ-45 jacks and are often labeled *Category 5* or *Cat 5* wire).
