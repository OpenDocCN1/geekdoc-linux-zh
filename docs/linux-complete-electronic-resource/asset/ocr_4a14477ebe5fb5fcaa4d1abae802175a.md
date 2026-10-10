Boot into Linux. During boot up a message like this should appear:

```
eth0: 3c509 at 0x300 tag 1, 10baseT port, address 00 20 af ee 01 23, IRQ 10. 3c509.c:1.07 6/15/95 becker@csdisi.gsfc.nasa.gov
```

If you missed it, type dmesg.

If you see a message like that, you are set and you can go to the next section. If you don't see a message like that, there are two possible explanations. The first is that your Ethernet card is PnP (Plug and Play) and you need to use tools, such as isapnp tools, to get it recognized. (I am not quite sure on this because I don't have a single PnP card, so correct me if I am wrong.) The other explanation is that you need to set up your card.

Most cards today come with DOS programs that are used to set up your card. For example, to get my 3COM 3c509 to work, all I need to do is boot into DOS and use a utility to configure my card. There is usually a Auto Configure option. If that does not solve your problem, try changing the IRQ for the card using the same utility. I find that usually IRQs 10, 11, and 12 work well. If none of this solves your problem, please read the Ethernet HOWTO referenced above or post to a newsgroup such as comp.os.linux.setup or comp.os.linux.networking.

# # Your ISP

If you think you have the card recognized, you now have to look at the entry for your ISP. I have sorted the information according to provider because setups are mostly ISP specific.

# ## MediaOne Express

MediaOne Express is an Internet cable service provided by MediaOne. The hardware setup consists of a cable modem produced by LanCiter or General Instruments, which plugs into an Ethernet card using a 10BaseT (UTP-45) cable. Assignment of IP addresses and other networking information is done using DHCP, which stands for Dynamic Host Configuration Protocol. The only thing you need to do is read the DHCP mini-HOWTO and configure your system appropriately. There is no other necessary configuration. The DHCP mini-HOWTO is Chapter 11 of this book, or you can find it at http://MetaLab.unc.edu/LDP/HOWTO/mini/DHCP.html.

Information about MediaOne Service can be found at http://www.mediaone.com.