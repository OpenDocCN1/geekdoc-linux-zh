
Linux uses *device files* to communicate with peripherals. Device files are found in the `/dev` directory and are roughly equivalent to Windows drivers: the Linux kernel uses them to communicate with your hardware.

You can connect your modem to one of four serial ports or one of many USB ports available on your PC. An external serial modem is generally connected to port `/dev/ttyS0`, and sometimes to `/dev/ttyS1`, or even `/dev/ttyS2` or `/dev/ttyS3`; USB modems are connected to `/dev/ttyUSB0`, `/dev/ttyUSB1`, and so on. If you have an internal modem, it can be any one of the `tty` devices.

## Firing Up Your Internet Connection

Fedora Core provides a PPP dialer utility to help you establish a PPP connection. You establish this connection by using the PPP configuration you set up with the Dialup Configuration tool (which we describe earlier in this chapter, in the section “Configuring Your Internet Connection”).

To connect to the Internet with the PPP dialer, follow these steps:

- 1. Click the **GNOME Menu** button and choose **System Tools** :: **Network Device Control**.
  The Network Device Control window appears, displaying all the network interfaces you have.
- 2. Click the name of your modem (for example, `Myconnection`) and then click **Activate**.
  The Network Device Control utility dials and connects to your ISP.
- 3. When you finish using the Internet, click the **Deactivate** button in the **Network Device Control** window.
  Your connection terminates.

## Chapter 6
## Broadband Rocks!

### In This Chapter

- Understanding broadband Internet connections
- Using a cable modem connection
- Using a DSL modem connection

![](img/41feae212f5c6612ff709354891f7b39_88_0.png)

You’re probably familiar with the ubiquitous dial-up Internet connection: You log on to the Internet, hear that sreeching modem sound and — Presto! Whammo! — you’re online. If you’re lucky, the entire dial-up process takes less than a minute, but it can take longer. And then there are those Web pages that take so-o-o lo-o-o-o-ong to finish downloading. There is a better way to get connected — it’s called *broadband*, a generic term for high-speed connections via cable TV and digital subscriber lines (DSL). Cable connections are provided by cable television companies, and DSL by your telephone company. Both are much faster than dial-up connections, and both have their advantages and disadvantages.

![](img/41feae212f5c6612ff709354891f7b39_88_1.png)

The *broad* in broadband means that wires and cables that connect a modem to the Internet have a wide *bandwidth*; they can handle more data at faster speeds and with greater reliability. Plain old telephone service (POTS) was created for transferring analog voice data. Needless to say, POTS just doesn’t do as well as broadband when it comes to the Internet.

The two most popular broadband types are cable modems and DSL. Cable modems connect through your cable television lines while DSLs use POTS lines. Broadband connections work from roughly 100 kilobits per second (Kbps) to several million bits per second (Mbps). A *kilobit* is a thousand bits per second; a *megabit* is a million bits per second. That’s enough speed to transfer graphics-rich Web pages in a few seconds; it’s also enough to listen to several audio streams or to watch a low-resolution video stream.

![](img/41feae212f5c6612ff709354891f7b39_88_2.png)

We’re on the verge of wireless broadband. The idea is to connect directly to an ISP without wires or cables of any kind. Some companies (such as Starbucks®) already offer such service on the small scale. On the larger scale, towns such as Rio Rancho, NM are about to become their own ISP. In the future, ISPs will offer wireless coverage similar to wireless telephone service. Stay tuned.

If you're ready to make the switch to a DSL or cable Internet connection, believe us when we tell you that you'll never want to go back to a dial-up modem. This chapter describes how to obtain and configure a broadband connection.

![](img/41feae212f5c6612ff709354891f7b39_89_0.png)

We recommend avoiding ISDN (Integrated Services Digital Network), satellite, and mental-telepathy-based broadband Internet connections. ISDN technology is old, and cable and DSL are better. Satellite Internet connections, just now being introduced, suffer from intrinsic problems such as transmission delays (latency) that wreak havoc on your communications; unfortunately, you can't upgrade to the speed of light. Some people say that mental telepathy (MT) works great, but we've found it scrambles our data.

### DSL and Cable Connections: The Difference Is the Wiring

Although the voice-based telephone network is now modern in many ways, its underpinnings haven't fundamentally changed over the last century. The telephone network consists of pairs of copper wires, twisted into cables that connect homes and businesses to a telephone company's central offices (CO). The phone company uses switches in its COs to connect you to your destination when you make a call. The switches are designed to limit the range of frequencies (called *bandwidth* that a phone call can use. The bandwidth is enough to recognize a voice, but not much more. Those limits prevent today's analog modems from pushing more than approximately 56,000 bits per second, or 56 Kbps, through the telephone network. (That 56 Kbps speed varies, mostly downward, depending on the condition of the copper wires you're connected to.)

Two of the most commonly used broadband systems are

- **Digital subscriber lines (DSL):** DSL is designed to avoid the restrictions of the traditional telephone system by circumventing the low-speed voice switches at the Central Office (CO). DSL uses the existing telephone wires, which connect your home to the nearest CO, to carry your Internet communication. After you're connected to the CO, however, your Internet communication is routed through a high-speed digital switch rather than through the voice equipment. By avoiding the voice equipment, you can achieve many times the speed of a dial-up modem.
  The main limitation of DSL is that traditional copper wire can carry a high-speed connection for only a few miles. Your telephone company can tell you whether it can provide you with DSL service.
- **Cable television networks:** Although cable television (CATV) companies don’t provide service to as many residences and businesses as the telephone companies do, their networks are not limited by historical constraints and are generally much faster than DSL. CATV networks also don’t have the 3- to 4-mile limits that DSL has. Typically, you can get an Internet connection through your CATV company if the company offers it — and only if the company serves your neighborhood.

## The Cable-Modem Option

Cable television companies have invested lots of capital to upgrade their networks in order to gain Internet market share. Their effort has paid off for consumers, and many places in the United States now have access to high-speed Internet connections at fairly reasonable prices.

However, you have to consider some downsides:

- Unfortunately, not all cable companies have caught up with 21st-century technology. Some CATV companies provide TV service but no Internet connections.
- Many people don’t live in areas served by cable TV. Internet cable is also not a good medium for providing services such as Web page hosting.
- Your cable company may require you to connect to its ISPs (or use an independent ISP that it approves of). Many people like to use an independent ISP because they’re familiar with it or it provides better service. Using your own ISP also makes it easier to set up your computer (or network) to provide services going out to the Internet. Cable companies cannot prevent you from using a different local ISP, but they don’t charge you less — so you end up paying for two services, one of which you’re not using.
- Relatively few cable companies directly support Linux. You may get a connection, but you’re on your own if you need to troubleshoot problems, even problems that have nothing to do with Fedora Core but still affect your machine.

If you decide that cable access is the right choice for your Internet access needs, here’s an overview of the process for connecting your Fedora Core computer to the Internet via a cable modem:

- 1. **Do some research and subscribe to an ICP service.**
  Locate an Internet cable provider (ICP) — usually that means your existing cable TV company — and subscribe to its ICP service.
