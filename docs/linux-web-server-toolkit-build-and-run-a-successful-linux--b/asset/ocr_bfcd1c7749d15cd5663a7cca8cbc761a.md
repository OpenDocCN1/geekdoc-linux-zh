# Linux Web Server Toolkit

The increasing speeds of modems may lead you to think that they are adequate for small Web sites. That's true to some extent, but be prepared to get more modems if traffic grows. The bigger problem is that modems always use an analog connection – a voice telephone line. An analog connection is inherently less stable than a digital connection. You have to monitor a modem connection yourself and reestablish it if it goes down; the telephone carrier won't watch for it as it would with a leased line or digital shared circuit.

The latest modems running at 56K have reached the theoretical limit of voice telephone line communication speed. In, the fine print will tell you, you get 56KB of throughput only if you have certain digital connections in between your modem, the telephone company central office, and the provider you're calling. If your telephone company has no digital equipment in your area, the multiple analog switches and connections will degrade the signal down to 33.6K.

The true throughput of a 33.6K modem – or any modem, for that matter – can be much higher using the compression algorithms that are part of most communications. A compression rate of two is common for most transfers.

So up, a modem uses a shared analog connection with inexpensive hardware. It connects to a serial port on your Linux system and requires no additional hardware or driver configuration.

So, can you use a modem to connect your Web server to the Internet? Yes, you can use under the following conditions:

+   * You anticipate low traffic to your site (under 5,000 hits per day or fewer).
* Your Web pages are small (under 15KB on average), and they incorporate few and small graphics.
* You can live with occasional downtime for your Web server when the phone connection is dropped.

On the upside, using a modem for a Web server provides the following advantages:

+   * You can set up the modem on your side in a matter of minutes.
* The setup on the ISP's site is just as easy.
* Your initial costs are much lower than other options. You need only the modem – no additional cards or routers.
* Your connection to the ISP will be much cheaper