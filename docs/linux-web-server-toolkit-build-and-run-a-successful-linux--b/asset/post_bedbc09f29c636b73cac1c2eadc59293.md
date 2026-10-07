
# Chapter 7: Connecting to the Internet

Dedicated leased line

![](img/e01f1106dd2902613fa07890c8baa7e6_202_0.png)

Figure 7-2: Dedicated circuits use one physical wire from one point to another point. Shared circuits use the same wires as do many other connections, changing over time.

Shared connections are adequate for most connections. They cost much less than dedicated leased lines and provide flexibility when upgrading. The sections that follow describe the various types of shared connection technologies that you can choose from.

Shared circuits can be analog or digital. Digital circuits provide more stable, high-speed communication but usually take longer to install. Circuits can often be installed either by a local telephone company such as U.S. West, PacBell or Bell Atlantic or by a national carrier such as Sprint, depending on the type of circuit you want installed.

# MODEM

A modem is the last standby. You can get a good 33.6K modem for $150 and connect to the Internet using your voice telephone line. Figure 7-3 diagrams a standard modem connection.

![](img/e01f1106dd2902613fa07890c8baa7e6_202_1.png)

Figure 7-3: Standard modems provide a simple method of connecting to your ISP over an inexpensive voice phone line.

# Linux Web Server Toolkit

The increasing speeds of modems may lead you to think that they are adequate for small Web sites. That's true to some extent, but be prepared to get more modems if traffic grows. The bigger problem is that modems always use an analog connection – a voice telephone line. An analog connection is inherently less stable than a digital connection. You have to monitor a modem connection yourself and reestablish it if it goes down; the telephone carrier won't watch for it as it would with a leased line or digital shared circuit.

The latest modems running at 56K have reached the theoretical limit of voice telephone line communication speed. In, the fine print will tell you, you get 56KB of throughput only if you have certain digital connections in between your modem, the telephone company central office, and the provider you're calling. If your telephone company has no digital equipment in your area, the multiple analog switches and connections will degrade the signal down to 33.6K.

The true throughput of a 33.6K modem – or any modem, for the matter – can be much higher using the compression algorithms that are part of most communications. A compression rate of two is common for most transfers.

So, a modem uses a shared analog connection with inexpensive hardware. It connects to a serial port on your Linux system and requires no additional hardware or driver configuration.

So, can you use a modem to connect your Web server to the Internet? Yes, you can use it under the following conditions:

- You anticipate low traffic to your site (under 5,000 hits per day or fewer).
- Your Web pages are small (under 15KB on average), and they incorporate few and small graphics.
- You can live with occasional downtime for your Web server when the phone connection is dropped.

On the upside, using a modem for a Web server provides the following advantages:

- You can set up the modem on your side in a matter of minutes.
- The setup on the ISP's site is just as easy.
- Your initial costs are much lower than other options. You need only the modem – no additional cards or routers.
- Your connection to the ISP will be much cheaper.
- Problems with modem connections are rare and easier to diagnose and fix than the other systems described in the following sections (but modem problems are yours, not the phone company's).

# FRAME RELAY

Frame-relay technology allows you to connect into a shared digital “cloud,” to the multiplexed voice telephone conference shared earlier. Frame relay hardware consists of a single board in your Linux PC. A CSU/DSU (connection service unit/data service unit) is also required. It can be purchased separately or as part of the newer frame relay boards on the market.

You can generally choose a speed for your line by 56K and T1 speeds (see “T1 and T3” for T1), but because the connection is shared by many multiplexed users, you never have full bandwidth - in fact, you never really do. You can sign up for a certain burst rate and a guaranteed sustained rate. The telephone company assigns groups of people to different sets of shared lines to balance loads. But if someone in the group is making a huge download (which is called bursting), you can't burst at the same time because there's not much bandwidth left. The downside of what remains is a very good system. Frame relay connections offering the benefits:

- Connections are highly reliable, much more so than modems because frame relay is digital and the connection is continually monitored by the telephone carrier.
- Relay permits higher speeds than most modems, and its packet-oriented data stream (compared to character-oriented modems) makes for speed, more efficient handling by your web server.
- Frame relay costs much less than your telephone connection (less than $100 per month fixed cost for 56K line).
- Connection equipment is inexpensive (way under $1000 for 56K speeds).

One drawback of frame relay – you just have to hope it's available where you live. Frame relay connections are gaining in popularity in some parts of the U.S. because they offer a digital shared connection at a very reasonable cost. Unfortunately, they are not available in all areas. Linux supports frame relay, as described later in this chapter.

# ISDN

ISDN, which stands for Integrated Services Network, provides two digital channels of 64K each for a total of 128K. ISDN uses a switched digital circuit like a modem (see 7-3), but is more flexible than either a modem or frame relay.

The downside of ISDN is the cost. Above and beyond the cost of installation, ISDN is almost always charged per minute. While these charges may not be a problem for an end user browsing the Web at home, they may make it unwieldy for businesses. ISDN has been getting a lot of press for years, and it's finally starting to become a reality in most parts of the country. ISDN has been especially popular in Europe and Japan, where phone booths already include ISDN. Linux supports numerous ISDN boards. Many are manufactured in Europe.

# T1 AND T3

T1 and T3 connections, and their siblings and pseudonyms, OC3, E3, and other high-speed digital connections would be the most popular if money were not an issue. A T1 connection provides 1.544MB per second, equivalent to 24 voice lines, or 43 times the bandwidth of a 33.6 modem. A T3 connection provides 45MB per second, or more than 1300 times the bandwidth of a 33.6 modem.

T1 and T3 connections are appropriate for organizations that anticipate huge amounts of Web site and related FTP and e-mail traffic. Large installations with 100,000 hits per day and hundreds of megabytes per day in file transfers should have a T1 connection. A stable T3 connection transfers several hundred gigabytes each day without choking. The Internet backbone used T3 lines for a backbone. It has moved to bigger things, but larger ISPs regularly use T3 lines to connect to the backbone.

A T1 connection can be created using a dedicated leased line to your ISP or a shared technology such as frame relay. Be sure that if you have leased a T1 line to your ISP, the ISP has at least much bandwidth to the Internet backbone.

The stability of T1 lines is very good, as with the other digital services, though maintenance can be tricky because of the special equipment and very high speeds.
