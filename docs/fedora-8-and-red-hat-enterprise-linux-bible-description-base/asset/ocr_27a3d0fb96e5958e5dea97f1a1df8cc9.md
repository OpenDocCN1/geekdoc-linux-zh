the PPP interface is started. After some parameter negotiations, the server assigns IP addresses to both sides of the communication, and the connection is ready to use. 
If you do get connected, but none of your applications (Web browser, FTP, and so on) seem to work, check that your PPP interface is noted as the default route (`/sbin/route -n`). If it is, check that you have the DNS servers specified correctly in your `/etc/resolv.conf` file. 
Use the `ping` command on those DNS servers’ IP addresses to make sure you can get through.

# # Connecting Your LAN to the Internet

The users on your LAN are happy if you made it so that they can share files and printers with each other. With your users already connected on a LAN, the next logical step is to set up a connection to the Internet that everyone can share. The advantages of doing this are as follows:

+   • **Save on modems** — Instead of each computer having its own modem, you can have one high-speed device (such as a DSL router or cable modem) that routes all traffic to the Internet.
+   
+   • **Save on telephone lines** — Instead of using a telephone line for each person who wants to get to the Internet, you can use one line to your ISP. (In the case of DSL, the telephone company will even let you use the same telephone line for both analog voice and high-speed digital data.)
+   
+   • **Central maintenance** — If information related to your Internet connection changes (such as your dial-out number or name server addresses), you can administrate those changes in one location instead of having to change it on every computer.
+   
+   • **Central security** — You can better control the Internet traffic that comes in to and goes out of your network.

The procedures in this section assume that you have already set up a LAN, as described in Chapter 15. It is also assumed that you have an outgoing connection from your Linux system to the Internet that all traffic between the computers on your LAN and the Internet can pass through. That outgoing connection may be dial-up or may come through another LAN card connected (to a DSL router) or other LAN. This section describes two ways to set up your Linux system so clients on the LAN can access the Internet:

+   • **As a router** — By configuring Linux as a router, it can route IP packets from clients on the LAN to the Internet through the dial-up connection.
+   
+   • **As a proxy server** — You can configure Linux as a proxy server. In this way, client computers on your LAN can access the Internet as though the connection were coming from the Linux computer.