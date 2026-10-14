
(cable modems), possibly a bit more work in the case of wireless and mobile connections, and sometimes a bit of a challenge when it comes to dial-up connections. In this chapter you will learn how to set up these connections, and in the next chapter you will learn a bit about what Linux has to offer in terms of the most commonly used Internet applications.

## How Do You Connect?

The way you go about setting up your connection really depends on how you’re trying to connect to the Internet. Here’s a list to help you decide which method to use:

- If you connect your computer to a wall socket, a router, or a cable modem by using an Ethernet cable, go to “Setting Up a Wired Connection” on page 46.
- If you connect to a wireless network or your own wireless router, head to “Setting Up a Wireless Connection” on page 49.
- If you connect using a dial-up modem connected to your phone line, the section “Setting Up a Dial-up Connection” on page 53 is the one for you.
- If you have an ADSL or DSL modem that is built in to your computer or connects to a USB port, try “Connecting with a DSL or ADSL Modem” on page 52.
- If you connect using a mobile (3G) broadband connection that plugs in to your computer, skip to “Mobile (3G) Broadband Connections” on page 55.

## Setting Up a Wired Connection

If you have a high-speed Internet connection from your cable television company or ISP or if you are connected to the Internet by a LAN at your office, you are really in luck, because these setups are probably the easiest to deal with. I’m going to assume that you’ve already set up your router or modem according to your Internet provider’s instructions, so all that remains is to connect an Ethernet cable between the modem/router (or LAN wall socket) and your computer’s network socket. After you’ve done that, you should be ready to go without any further settings to fool with.

## Checking Your Connection

If you like, you can see whether you’re connected by opening Firefox (click the Firefox launcher in the top panel, right next to the System menu) and then, once it starts up, trying to navigate to a common site, such as http://www.yahoo.com/. If the site comes up, you know you’re all set.

If you have a problem getting online and you are trying to connect via a LAN or cable modem, you could try to refresh your connection by right-clicking the Network Manager icon in the top panel, unchecking the **Enable Networking** box in the pop-up menu, waiting a few seconds, and then checking the **Enable Networking** box in the pop-up menu again. If that doesn’t work, try restarting your machine while physically connected to your Internet source with the Ethernet cable. If the lack of connectivity persists, it is possible that your network card is not supported by Linux. This is relatively rare but, fortunately, easily remedied (by replacing it).

The problem could also be that your network or service provider does not automatically assign addresses via Dynamic Host Configuration Protocol (DHCP). *DHCP* is a means by which your Internet provider can automatically provide your system with the configuration information it needs in order to connect to the Internet. If your provider does not use DHCP, you will have to get the necessary information about settings from the network administrator or service provider and enter the settings yourself.

## Setting Up a Cable or Ethernet Connection for Providers Not Using DHCP

To input your cable or Ethernet settings yourself, first get the settings you need from your network administrator or Internet provider, and then perform the following steps:

1. Select **System › Preferences › Network Connections**.
2. Choose the **Wired** tab (Figure 4-1), and select the network connection from the list by clicking it once (it should have a name like *Auto eth0*). If there are no entries in the list, then your network card hasn’t been properly recognized. Take a look at “Installing Drivers for Your Network/Wireless Card” on page 390 to see how to fix this.

![](img/f7cef0df22f9dba5a41777808c98eece_84_0.png)

*Figure 4-1: The Network Connections window*

3. Click **Edit**, and you’ll be presented with a settings window. Choose the **IPv4 Settings** tab, and change the Method setting from Automatic (DHCP) to **Manual**.
