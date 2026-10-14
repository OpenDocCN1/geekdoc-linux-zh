
Google. In this case, the problem might be with your DNS settings or some other software, rather than your connection or your network/wireless card. If you get any other message, you probably aren’t connected to the Internet, so it could be a hardware problem.

![](img/f7cef0df22f9dba5a41777808c98eece_426_0.png)

Figure 21-9: The results of pinging one of Google’s servers if you have a working Internet connection

## Is your card recognized?

Open a Terminal, and type lshw -c network -short, and press ENTER. A list of the network and wireless cards that were recognized on your computer will be displayed, similar to the one shown in Figure 21-10; check whether any of them have a description matching the make or model of your card. If they do, the card has been recognized but may not necessarily have the right drivers.

![](img/f7cef0df22f9dba5a41777808c98eece_426_1.png)

Figure 21-10: The list of recognized network and wireless cards on my computer

## Is your card turned on?

If you have a wireless card, it may have been turned off. See the instructions in “No Wireless Networks Are Found” on page 392 for advice on how to check whether this is the case.

## Are you using the right drivers?

Ubuntu sometimes uses the wrong driver for a network/wireless card. To check which driver is being used for your card, open a Terminal, and type lshw -c network followed by ENTER. Scroll down through all of the text, and find the card that has a product or vendor matching those of your card. Then, scroll down a few more lines until you get to the configuration line. This will tell you which driver is being used and the version number of the driver. You can compare this with the information for your card at https://wiki.ubuntu.com/HardwareSupportComponentsWiredNetworkCards/ (for wired network cards) or https://help.ubuntu.com/community/WifiDocs/WirelessCardsSupported/ (for wireless cards).

## Have you checked your settings?

Select System ▸ Preferences ▸ Network Connections, and find the entry for your connection on the appropriate tab. Then, select the connection, and click Edit. Check through the settings in the Editing window to see whether any of them are wrong—the usual suspects are your default gateway and DNS servers (if you have a manually configured wired network) and the wireless security key (if you have a wireless connection).

For those of you struggling with a wireless connection, you can find a wireless troubleshooting guide at https://help.ubuntu.com/community/WifiDocs/WirelessTroubleShootingGuide/. It’s quite technical in places, though, so you might prefer to ask for help on the Ubuntu forums.

## Installing Drivers for Your Network/Wireless Card

If your network card or wireless card hasn’t been recognized or isn’t working as expected, you might need to install some different drivers for it. You can try a few methods, and the one that works will very much depend on the make and model of your card. I’ve included two of the most general ones in the following sections, but some cards need you to follow very specific instructions to get them working. The lists at https://wiki.ubuntu.com/HardwareSupportComponentsWiredNetworkCards/ (wired cards) and https://help.ubuntu.com/community/WifiDocs/WirelessCardsSupported/ (wireless cards) should be able to help you figure out which method to use.

## Check for Restricted Drivers

Some network/wireless cards have restricted drivers that you can download to get your card working. These drivers are normally provided by the manufacturer of the card and are “restricted” in the sense that they can’t be fixed by Ubuntu developers if something goes wrong with them (in other words, they’re not open source).

You need to be connected to the Internet to download restricted drivers. If you don’t have a working connection (probably because you’re currently in the process of trying to get your card working!), try using an Ethernet cable to plug the computer directly into your wireless router or cable modem (see Chapter 4 for more information). This will work only if you have a functioning wired network card. If your wired network card doesn’t work, you won’t be able to follow these instructions.
