In dialup networking, both your PC and the remote system run network protocol (called TCP/IP) software. When your PC dials up and sets up a communication path, the network protocols exchange data packets over that dialup connection. The neat part is that any number of applications can use the same dialup connection to send and receive data packets. So your PC becomes a part of the network to which the remote computer belongs. (If the remote computer is not on a network, dialup networking creates a network that consists of the remote computer and your PC.)

In Chapter 2 of this minibook, I describe TCP/IP protocol some more, but I have to use the term as well as a few concepts such as *Internet Protocol* (IP) address and *Domain Name Service* (DNS) when describing how to set up dialup networking.

![](bbox=[0.14, 0.43, 0.23, 0.54])

Setting up a TCP/IP network over a dialup link involves specifying the protocol — the convention — for packaging a data packet over the communication link. *Point-to-Point Protocol* (PPP) is such a protocol for establishing a TCP/IP connection over any point-to-point link, including dialup phone lines. Linux supports PPP, and it comes with the configuration tools you can use to set up PPP so that your system can establish a PPP connection with your ISP.

Here’s what you have to do to set up dialup networking in Linux:

+   1. Install an internal or external modem in your PC. If your PC did not already come with an internal modem, you can buy an external modem and connect it to the PC’s serial or USB port.
+   2. Connect the modem to the phone line and power up the modem.
+   3. Get an account with an ISP. Every ISP provides you a phone number to dial, a username, and a password. Additionally, the ISP gives you the full names of servers for e-mail and news. Typically, your system automatically gets an IP address.
+   4. Run a GUI tool (if available) to set up a PPP connection. If you cannot find a GUI tool, type **wvdialconf** or **etc/wvdial.conf** at the shell prompt. The `wvdialconf` program automatically detects the modem and sets up the configuration file `/etc/wvdial.conf`. Now use a text editor to edit the file `/etc/wvdial.conf` and enter the ISP’s phone number as well as the username and password of your Internet account with the ISP. (You can guess where to enter these items, just look for the fields labeled Username, Password, and Phone.)
+   5. Use a GUI tool (if available) to activate the PPP connection to connect to the Internet. If there is no GUI tool, log in as `root` and type `wvdial` to establish the PPP connection.

I briefly go over these steps in the following sections.