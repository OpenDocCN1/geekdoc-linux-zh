
## What Is the Internet?

How you view the Internet depends on your perspective. Regular folks see the Internet in terms of the services they use. For example, as a user, you might think of the Internet as an information-exchange medium with features such as

- **E-mail:** Send e-mail to any other user on the Internet, using addresses such as `mom@home.net`.
- **Web:** Download documents and images from millions of servers throughout the Internet.
- **Newsgroups:** Read newsgroups and post news items to newsgroups with names such as `comp.os.linux.networking` or `comp.os.linux.setup`.
- **Information sharing:** Download software, music files, videos, and so on. Reciprocally, you may provide files that users on other systems can download.
- **Remote access:** Log on to another computer on the Internet, assuming that you have access to that remote computer.

The techies say that the Internet is a worldwide *network of networks*. The term *internet* (without capitalization) is a shortened form of *internetworking* — the interconnection of networks. The Internet Protocol (IP) was designed with the idea of connecting many separate networks.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_120_0.png)

In terms of physical connections, the Internet is similar to a network of highways and roads. This similarity is what has prompted the popular press to dub the Internet “the Information Superhighway.” Just as the network of highways and roads includes some interstate highways, many state roads, and many more residential streets, the Internet has some very high-capacity networks (for example, a 10 Gbps backbone can handle 10 billion bits per second) and a large number of lower-capacity networks ranging from 56 Kbps dialup connections to 45 Mbps T3 links. (Kbps is thousand-bits-per-second, and Mbps is million bits per second.) The high-capacity network is the backbone of the Internet.

In terms of management, the Internet is not run by a single organization, nor is it managed by any central computer. You can view the physical Internet as a “network of networks” managed collectively by thousands of cooperating organizations. Yes, a collection of networks managed by *thousands* of organizations — sounds amazing, but it works!

## Deciding How to Connect to the Internet

So you want to connect to the Internet, but you don’t know how? Let me count the ways. Nowadays you have three popular options for connecting home offices and small offices to the Internet (of course, huge corporations and governments have many other ways to connect):

- **Digital Subscriber Line (DSL):** Your local telephone company, as well as other telecommunications companies, may offer DSL. DSL provides a way to send high-speed digital data over a regular phone line. Typically, DSL offers data-transfer rates of between 128 Kbps and 1.5 Mbps. You can download from the Internet at much higher rates than when you send data from your PC to the Internet (*upload*). One caveat with DSL is that your house must be between 12,000 and 15,000 feet from your local central office (the phone-company facility where your phone lines end up). The distance limitation varies from provider to provider. In the United States, you can check out the distance limits for many providers at www.dslreports.com/distance.
- **Cable modem:** If the cable television company in your area offers Internet access over cable, you can use that service to hook up your Linux system to the Internet. Typically, cable modems offer higher data-transfer rates than DSL — for about the same cost. Downloading data from the Internet via cable modem is much faster than sending data from your PC to the Internet. You can expect routine download speeds of 1.5 Mbps and upload speeds of around 128 Kbps, but sometimes you may get even higher speeds than these.
- **Dialup networking:** A dialup connection is what most folks were using before DSL and cable modems came along. You hook up your PC to a modem that’s connected to the phone line. Then you dial up an ISP to connect to the Internet. That’s why it’s called *dialup networking* — establishing a network connection between your Linux PC and another network (the Internet) through a dialup modem. In this case, the maximum data-transfer rate is 56 Kbps.

DSL and cable modem services connect you to the Internet and also act as your Internet service provider (ISP); in addition to improved speed, you pay for an IP address and your e-mail accounts. If you use a dialup modem to connect to the Internet, first you have to connect to the phone line (for which you pay the phone company) and then select and pay a separate ISP — which gives you a phone number to dial and all the other necessary goodies (such as an IP address and e-mail accounts).

Table 7-1 summarizes all these options. You can consult that table and select the type of Internet connection that’s available to you and that best suits your needs.

| Feature | Dialup | DSL | Cable |
|---|---|---|---|
| Equipment | Modem | DSL modem, Ethernet card | Cable modem, Ethernet card |
| Also requires | Phone service and an Internet service provider (ISP) | Phone service and location within 12,000 to 15,000 feet of central office | Cable TV connection |
| Connection type | Dial to connect | Always on, dedicated | Always on, shared |
| Typical speed | 56 Kbps maximum | 640 Kbps download, 128 Kbps upload (higher speeds cost more) | 1.5 Mbps or higher download, 128 Kbps upload |
| One-time costs (estimate) | None | Install = $100–$200 (none for self install); Equipment = $50–$100 (may be leased and may require activation cost) | Install = $100–$200 (none for self install); Equipment = $50–$100 (may be leased) |
| Typical monthly cost (2005) | Phone charges = $20/month; ISP charges = $15–$30/month | $40–$50/month; may require monthly modem lease | $40–$50/month; may require monthly modem lease |

*Note: Costs vary by region and provider. Costs shown are typical ones for U.S. metropolitan areas.*

## Connecting to the Internet with DSL

DSL (Digital Subscriber Line) uses your existing phone line to send digital data in addition to the normal analog voice signals (analog means continuously varying, whereas digital data is represented by 1s and 0s). The phone line goes from your home to a central office where the line connects to the phone company's network — by the way, the connection from your home to the central office is called the local loop. When you sign up for DSL service, the phone company hooks up your phone line to some special equipment at the central office. That equipment can separate the digital data from voice. From then on, your phone line can carry digital data that is then directly sent to an Internet connection at the central office.

### How DSL works

A special box called a DSL modem takes care of sending digital data from your PC to the phone company’s central office over your phone line. Your PC can connect to the Internet with the same phone line that you use for your normal telephone calls — you can make voice calls even as the line is being used for DSL. Figure 7-1 shows a typical DSL connection to the Internet.

Your PC talks to the DSL modem through an Ethernet connection, which means that you need an Ethernet card in your Linux system.

Your PC sends digital data over the Ethernet connection to the DSL modem. The DSL modem sends the digital data at different frequencies than those used by the analog voice signals. The voice signals occupy a small portion of all the frequencies that the phone line can carry. DSL uses the higher frequencies to transfer digital data, so both voice and data can travel on the same phone line.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_123_0.png)

**Figure 7-1:** DSL provides high-speed connection to the Internet over a regular phone line.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_124_0.png)

The distance between your home and the central office — the *loop length* — is a factor in DSL’s performance. Unfortunately, the phone line can reliably carry the DSL signals over only a limited distance — typically 3 miles or less, which means that you can get DSL service only if your home (or office) is located within about 3 miles of your phone company’s central office. Your phone company can tell you whether your location can get DSL or not. Often, it has a Web site where you can type in your phone number and get a response about DSL availability. For example, try www.dslavailability.com for U.S. locations.

### Stirring the DSL alphabet soup: ADSL, IDSL, SDSL

I have been using the term *DSL* as if there was only one kind of DSL. As you may imagine, nothing is ever that simple. DSL has in fact three variants, each with different features. Take a look.

- **ADSL:** Asymmetric DSL, the most common form of DSL, has much higher download speeds (from the Internet to your PC) than upload speeds (from your PC to the Internet). ADSL can have download speeds of up to 8 Mbps and upload speeds of up to 1 Mbps. ADSL works best when your location is within about 2½ miles (12,000 feet) of your central office. ADSL service is priced according to the download and upload speeds you want. A popular form of ADSL, called G.lite, is specifically designed to work on the same line you use for voice calls. G.lite has a maximum download speed of 1.5 Mbps and a maximum upload speed of 512 Kbps.
- **IDSL:** ISDN DSL (ISDN is an older technology called *Integrated Services Digital Network*) is a special type of DSL that works at distances of up to 5 miles between your phone and the central office. The downside is that IDSL only offers downstream (from the Internet to your PC) and upstream (from your PC to the Internet) speeds of up to 144 Kbps.
- **SDSL:** Symmetric DSL provides equal download and upload speeds of up to 1.5 Mbps. SDSL is priced according to the speed you want, with the higher speeds costing more. The closer your location is to the phone company’s central office, the faster the connection you can get.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_124_1.png)

DSL speeds are typically specified by two numbers separated by a slash, like this: 1500/384. The numbers refer to data-transfer speeds in kilobits per second (that is, thousands-of-bits per second, abbreviated as Kbps). The first number is the download speed; the second the upload. Thus 1500/384 means you can expect to download from the Internet at a maximum rate of 1,500 Kbps (or 1.5 Mbps) and upload to the Internet at 384 Kbps. If your phone
