
## 278 Connecting with DSL

Here are some key points to note in Figure 1-2:

- Connect your DSL's data connection to the phone jack on a wall plate.
- Connect the DSL modem's Ethernet connection to the Ethernet card on your PC.
- When you connect other telephones or fax machines on the same phone line, install a microfilter between the wall plate and each of these devices.

![](img/d9230b719dc0efd80851f363d8c6f571_304_0.png)

Because the same phone line carries both voice signals and DSL data, you need the microfilters to protect the DSL data from possible interference. You can buy them at electronic stores or from the DSL modem.

![](img/d9230b719dc0efd80851f363d8c6f571_304_1.png)

When you connect your Fedora Core PC to the Internet with DSL, the connection is always on — and with more potential for outsiders to break into the PC. You need to make sure that the Fedora Core firewall is set to High Security. To configure the firewall settings, choose Menu:System Settings:Security Level from the GNOME desktop.

You can protect your Fedora system from intruders, and as an bonus, share the high-speed connection with other PCs in a local-network (LAN). You need a router that can perform Network Address Translation (NAT). Such a router translates multiple Internet Protocol (IP) addresses from an internal LAN into a single IP address, which allows all the internal PCs to access the Internet.

If you want to set up a local-area network, you will need an Ethernet hub to connect the other PCs to the network. Figure 1-3 shows a typical setup that connects a LAN to the Internet through a NAT router and a DSL modem.

Here are the points to note when setting up a connection like the one shown in Figure 1-3:

- You need a NAT router with two 10BaseT Ethernet ports (the BaseBaseT port looks like a large phone jack, also known as an RJ45 jack). Typically one port is labeled Ethernet (External or WAN for wide-area network) and the other is labeled Local or LAN (for local-area network).
- You also need an Ethernet hub. For a small home network, you can buy a 4- or 8-port Ethernet hub. Basically, you want a hub with as many ports as the number of PCs you intend to connect to your local-area network.
- Connect the Ethernet port of the DSL modem to the Internet port of the NAT router, using a 10BaseT Ethernet cable (these like phone wires with bigger RJ-45 jacks and are often labeled Category 3 or Cat 5 wire).
- Connect the Local Ethernet port of the NAT router to one of the ports on the Ethernet hub, using a 10BaseT Ethernet cable.

![](img/d9230b719dc0efd80851f363d8c6f571_304_2.png)

## Connecting with a Cable Modem 279

Now connect each of the PCs to the Ethernet hub. (Of course, to do so you must first have an Ethernet card installed and configured in each PC.)

Phone jack
Ethernet cables (10BaseT)
Ethernet hub

![](img/d9230b719dc0efd80851f363d8c6f571_305_0.png)

You can also buy a NAT router with a built-in 4- or 8-port Ethernet hub. With such a combined router-hub, you need only one box to set up a LAN and connect it to the Internet via a DSL modem. These boxes are typically sold under the name Cable/DSL router because they work with both DSL and a cable modem.

> TIP
> Consult Chapter 2 of this minibook for information on how to configure on the Fedora Core system so your system can access the Internet.

DSL providers typically use a protocol called PPP over Ethernet (PPPoE) to establish a connection between your PC and the equipment at the provider's central office. PPPoE requires you to use a username and password to set up the connection over Ethernet. To set up your system you all have to select Main Menu→System Tools→Internet Configuration Wizard and click xDSL connection from the list. Then go through the successive screens and provide the requested information as login name and password.

> REMEMBER
Book IV
Chapter 1

## Connecting with a Cable Modem

Cable TV companies also offer high-speed Internet access over the same coaxial cable that carries television signals to your home. After the cable company installs the necessary equipment at its facility to send and receive digital data over the coaxial cables, customers can sign up for cable Internet service. You can then get high-speed Internet access over the same cable that delivers TV signals to your home.

## How cable modem works

A box called a cable modem is at the heart of Internet access over the cable TV network takes digital data from your PC's Ethernet card and puts it in an unused block of frequency (think of it as another TV channel, but instead of pictures and sound, this channel carries digital data.

![](img/d9230b719dc0efd80851f363d8c6f571_306_0.png)

Figure 1-4: Cable modems provide high-speed Internet access over the cable TV network.

## Connecting with a Cable Modem 281

The cable modem uses a standard called DOCSIS, which stands for Data Over Cable Service Interface. This standard allows cable modems to communicate with the cable provider's headend. The modem translates the digital data from your PC into signals that can be sent over the coaxial cable, and vice versa.

The cable modem uses different frequency bands for downstream and upstream data. The downstream data is the data coming from the provider to your PC, while the upstream data is the data sent from your PC to the provider. The downstream speeds are typically much higher than the upstream speeds.

The cable modem also uses encryption to protect your data from being intercepted. This ensures that your internet traffic cannot be seen by other users who are also on the same cable network.

If you want to check your downstream speed, go to speedtest.net and click the link. This will give you an estimate of your connection speed.

## 282 Connecting with a Cable Modem

### Typical cable modem setup

To set up cable modem access, your TV provider must offer highspeed Internet access. If the service is available, you can call to sign up. The cable companies often have promotional offers such as no installation fee or a reduced rate for three months. Look for these offers.

The installation is typically done by a technician, who splits your incoming cable into two — one side goes to the TV and the other to the cable modem. The technician provides information about the cable modem to the cable company's head for set up at its end. When it is all done, you can plug-in your PC's Ethernet card to the cable modem and you're all set to enjoy high-speed Internet access. Figure 1-5 shows a typical cable-modem hookup.

![](img/d9230b719dc0efd80851f363d8c6f571_308_0.png)

Figure 1-5:
The cable TV signal is split between the TV and the cable modem.

The cable modem connects to an Ethernet card in your PC. If you don't have an Ethernet card in your PC, the cable company technician provides one.
