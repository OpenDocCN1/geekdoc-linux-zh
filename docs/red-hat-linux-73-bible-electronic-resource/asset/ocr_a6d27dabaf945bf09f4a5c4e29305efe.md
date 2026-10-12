The number of static IP addresses that you need varies, depending on how you configure your servers. Most likely, you want at least two static IP addresses, one for each of two DNS servers (if you're configuring DNS). In a small organization, those same servers may also offer your Web server, mail server, and other services as well. In general, you want one static IP address for each computer that you make publicly accessible to the Internet.

> **TIP:** You can do some tricks with services such as port forwarding (iptables in Chapter 14) and virtual hosting (Apache Web server in Chapter 21) that enable multiple physical computers to offer services on a single static IP address. These tricks can reduce the number of IP addresses you need to purchase. (To simplify the discussion in this chapter, however, I'm assuming at this point that each public server has its own static, public IP address.)

# ## Choosing a connection speed

Another difficulty of keeping your servers in your own home or business is choosing how fast an Internet connection you need. Although most data centers at ISPs offer more than enough bandwidth for your needs, high-speed Internet connections may not be available to your location — or may prove prohibitively expensive.

Although it’s technically possible, using a dialup connection (up to 56 Kbps) to support an Internet server is generally considered unacceptable. “Always-on” connection services that you may want to consider include the following:

+   - **Digital Subscriber Line (DSL):** DSL service is becoming widely available these days. Using only the standard telephone wiring in your home, you can maintain an always-on Internet connection and telephone service on the same wires. Speeds of between 640 Kbps and 7 Mbps are available with DSL service (although the actual speeds that you attain are typically slower than those in the advertisements).

+   - **Integrated Services Digital Network (ISDN):** ISDN has been around longer than DSL to offer high-speed network services, and it’s comparable to DSL in the speeds that it can offer. ISDN is, however, typically more expensive to implement than DSL at comparable speeds.

+   - **Frame Relay:** This service is a packet-switching protocol that runs across wide-area networks. Although it can prove much more expensive than either DSL or ISDN, it can achieve much higher rates of speed. Speeds can range from 56 Kbps to 1.544 Mbps — or even as much as 45 Mbps. Frame relay can operate across a variety of network mediums. One of its primary advantages is that it uses virtual circuits that offer a fixed rate of speed, because the circuit between you and the ISP isn't shared with other ISP customers.

If your business can support it, you may want dedicated T-1 or T-3 lines for your business. A T-1 connection can operate at data rates of 1.444 Mbps. A T-3 line can support rates of 43 Mbps. Check with your local ISPs for available connection types and pricing.