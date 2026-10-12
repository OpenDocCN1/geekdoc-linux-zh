
# Book IV

# Networking

![](img/9f89727199836b0f871f1745838aa8b2_295_0.png)

"It's okay. One of the routers must have gone down and we had a brief broadcast storm."

# Contents at a Glance

- Chapter 1: Connecting to the Internet....271
- Chapter 2: Setting Up a Local Area Network....295
- Chapter 3: Adding a Wireless Ethernet LAN...307
- Chapter 4: Managing the Network .........319
- Chapter 5: Cool Networking Projects.....329

# Chapter 1: Connecting to the *Internet*

## *In This Chapter*

- Understanding the Internet
- Deciding how to connect to the Internet
- Connecting to the Internet with DSL
- Connecting to the Internet with cable modem
- Setting up a dial-up PPP link

The Internet is fast becoming a lifeline for most of us. Seems we can’t get through a day without it (and I know I could not write this book without it). Sometimes I wonder how we ever managed without the Internet — and that you want to connect your Fedora Core system to the Internet is a pretty safe bet. In this chapter, I show you how to connect to the Internet in several different ways — depending on whether you have DSL, cable modem, or dial-up network connection.

Two of the options for connecting to the Internet — DSL and cable modem — involve connecting a special modem to an Ethernet card on your Fedora Core system. In these cases, you have to set up Ethernet networking on your Fedora Core system. (I explain networking in Chapter 2 of this minibook.) In this chapter, I show you in detail how to set up a DSL or a cable modem connection.

I also show you the other option — dial-up networking — that involves dialing up an Internet Service Provider (ISP) from your Fedora Core system.

## Understanding the Internet

How you view the Internet depends on your perspective. Common folks like us see the Internet in terms of the services we use. For example, as users we think of the Internet as an information-exchange medium — with features such as

- **E-mail:** Send e-mail to any other user on the Internet, using addresses such as mom@home.net.
- **Web:** Download and view documents from millions of servers throughout the Internet.
- **Newsgroups:** Read newsgroups and post news items to newsgroups with names such as comp.os.linux.networking or comp.os.linux.setup.
- **Information sharing:** Download software, music files, videos, and so on. Reciprocally, you may provide files that users on other systems can download.
- **Remote access:** Log on to another computer on the Internet, assuming that you have access to that remote computer.

The techies among us say the Internet is a worldwide network of networks. The term internet (without capitalization) is a short form of internetworking — the interconnection of networks. The Internet Protocol (IP) was designed with the idea of connecting many separate networks.

![](img/9f89727199836b0f871f1745838aa8b2_298_0.png)

In terms of physical connections, the Internet is similar to a network of highways and roads. This similarity is what has prompted the popular press to dub the Internet “the Information Superhighway.” Just as the network of highways and roads includes some interstate highways, many state roads, and many more residential streets, the Internet has some very high-capacity networks (for example, a 10-Gbps backbone can handle 10 billion bits per second) and a large number of lower-capacity networks ranging from 56 Kbps dial-up connections to 45 Mbps T3 links (Kbps is thousand-bits-per-second and Mbps is million-bits-per-second). The high-capacity network is the backbone of the Internet.

In terms of management, the Internet is not run by a single organization, nor is it managed by any central computer. You can view the physical Internet as a “network of networks” managed collectively by thousands of cooperating organizations. Yes, a collection of networks managed by *thousands* of organizations — sounds amazing, but it works!

## Deciding How to Connect to the Internet

So you want to connect to the Internet, but don’t know how? Let me count the ways. Nowadays you have three popular options for connecting homes and small offices to the Internet (*of course*, huge corporations and governments have many other ways to connect):

- **Digital Subscriber Line (DSL)**: Your local telephone company, as well as other telecommunications companies, may offer DSL. DSL provides a way to send high-speed digital data over a regular phone line. Typically, DSL offers data-transfer rates of between 128 Kbps and 1.5 Mbps. You can download from the Internet at much higher rates than when you send data from your PC to the Internet (upload). One caveat with DSL is that your home must be between 12,000 and 15,000 feet from your local central office (the phone-company facility where your phone lines end up). The distance limitation varies from provider to provider. In the United States, you can check out the distance limits for many providers at www.dslreports.com/distance.
- **Cable modem**: If the cable television company in your area offers Internet access over cable, you can use that service to hook up your Fedora Core system to the Internet. Typically, cable modems offer higher data-transfer rates than DSL — for the same cost. Downloading data from the Internet via cable modem is much faster than sending data from your PC to the Internet. You can expect routine download speeds of 1.5 Mbps and upload speeds of around 128 Kbps, but sometimes you may get even higher speeds than these.
- **Dial-up networking**: A dial-up connection is what most of us were using before DSL and cable modems came along. You hook up your PC to a modem that's connected to the phone lines. Then dial up an ISP to connect to the Internet. That's why it's called dial-up networking — establishing a network connection between your Fedora Core PC and another network (the Internet) through a dial-up modem. In this case, the maximum data-transfer rate is 56 Kbps.

DSL and cable-modem service connect you to the Internet and also act as your Internet Service Provider (ISP); in addition to improved speed, what you're paying for is an IP address and e-mail accounts. If you use a dial-up modem to connect to the Internet, first you have to connect to the phone line (for which you pay the phone company) and then select and pay a separate ISP — which gives you a phone number to dial and all the other necessary goodies (such as an IP address and e-mail accounts).

Table 1-1 summarizes all these options. You can consult that table and select the type of connection that's available to you and that best suits your needs.

| Feature | Dial-up | DSL | Cable |
|---|---|---|---|
| Equipment | Modem | DSL modem, Ethernet card | Cable modem, Ethernet card |
| Also requires | Phone service and an Internet Service Provider (ISP) | Phone service and location within 12,000 to 15,000 feet of central office | Cable TV connection |
| Connection type | Dial to connect | Always on, dedicated | Always on, shared |
| Typical speed | 56 Kbps maximum | 640 Kbps download, 128 Kbps upload (higher speeds cost more) | 1.5 Mbps download, 128 Kbps upload |
| One-time costs (estimate) | None | Install = $100-200; Equipment = $200-300 (may be leased and may require activation cost) | Install = $100-200; Equipment = $60-100 (may be leased) |
| Typical monthly cost (2004) | Phone charges = $20/month; ISP charges = $15-30/month | $50/month; may require monthly modem lease | $50/month; may require monthly modem lease |

Note: Costs vary by region and provider. Costs shown are typical ones for U.S. metropolitan areas.

## Connecting with DSL

DSL stands for Digital Subscriber Line. DSL uses your existing phone line to send digital data in addition to the normal analog voice signals (analog means continuously varying, whereas digital data is represented by 1s and 0s). The phone line goes from your home to a central office, where the line connects to the phone company's network — by the way, the connection from your home to the central office is called the local loop. When you sign up for DSL service, the phone company hooks up your phone line to some special equipment at the central office. That equipment can separate the digital data from voice. From then on, your phone line can carry digital data that is then directly sent to an Internet connection at the central office.

## How DSL works

A special box called a DSL modem takes care of sending digital data from your PC to the phone company's central office over your phone line. Your PC can connect to the Internet with the same phone line that you use for your normal telephone calls — you can make voice calls even as the line is being used for DSL. Figure 1-1 shows a typical DSL connection to the Internet.

Your PC talks to the DSL modem through an Ethernet connection, which means that you need an Ethernet card in your Fedora Core system.
