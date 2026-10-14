Linux is an excellent platform for exploring the online world and for providing Internet services of your own. As a personal “surfboard,” Red Hat Linux comes with everything you need to connect to an Internet service provider (ISP), including TCP/IP software; client programs such as FTP, Telnet, Finger, Mail, Ping, Lynx, and Netscape.

Linux also makes it easy to set up your own servers so you can operate FTP or Web sites and even provide Telnet or dial-up access to your system. If you have dreams of becoming an ISP, the Red Hat Linux product is an excellent platform to build on. The really nice thing is that TCP/IP and all the popular network services are installed automatically and preconfigured for you. If you’ve ever tried to configure a Unix network, set up email delivery, or get a Web server running, you will really appreciate this feature. (In technical terms, it means that local loopback, sendmail, inetd, httpd, and several other network daemons are configured and running when you boot up Red Hat Linux.)
In this chapter, you’ll learn the following:

+   - How to connect your Linux system to the Internet with a dial-up PPP connection
+   - What tools are available for Internet access (text and graphical)
+   - How to operate your own Internet site
+   - Where to get more information on Linux networking

# SETTING UP YOUR SERIAL PORT TO WORK WITH YOUR MODEM

By default, Red Hat Linux is configured to run your serial (modem) port at a speed of 9600 bps. But faster modems, with speeds of 33.6 and 56 Kbps, for instance, are quite common now. It would be a shame to spend money on a fast modem and not use it to the fullest, so to get the best performance, you’ll have to tweak your serial port settings.

Unless you have a very slow modem (9600 bps or less), you should use the setserial command to enable Linux to make a high-speed connection. Depending on your modem speed, at the command prompt