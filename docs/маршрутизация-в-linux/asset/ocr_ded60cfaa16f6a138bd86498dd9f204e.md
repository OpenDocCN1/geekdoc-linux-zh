Assuming there have been no compiler errors, you should now have the PoPToP binaries in /usr/local/bin. You also will need to be root to launch the PPTP daemon pptpd.

# Configuring and Debugging PoPToP

After everything has been compiled and installed, you'll need to edit three files to tweak everything for your installation. The files are /etc/pptpd.conf, /etc/ppp/chap-secrets, and /etc/ppp/options.

The /etc/ppp/chap-secrets is a text file containing the username, password, servername, and valid IP addresses that they can connect from. You'll want to add one or more users to this file so that they can connect to the server.

There is a sample /etc/pptpd.conf file included with the source download, which you can customize to your own tastes. You'll use this file to set the local and remote IP addresses, speed at which clients can connect, ports at which the daemon will listen, and debugging level. Make sure that you restart syslogd after starting pptpd to enable logging.

Finally, you'll need to edit /etc/ppp/options that is included with the source distribution to reflect the options in /etc/ppp/chap-secrets.

If you have any problems setting up PoPToP, you might want to check the PoPToP web site for troubleshooting tips or workarounds for particular clients. Right now there are several HOWTOs and setup guides for various Windows clients.

# Commercial VPN Solutions

If you're looking for a quick-and-easy solution to your routing and VPN needs, there are a few commercial solutions available that you might find easier to set up.

Most of these are based on the Open Source and Free Software tools but include slicker configuration tools. There are also some Linux-based hardware solutions that you might find to be interesting alternatives to Cisco routers.

# NetMAX VPN Server

One outstanding commercial product is the NetMAX VPN Server. It's a customized Linux distribution with web-based setup tools that allow you to quickly and easily set up an IPSec VPN solution. It also includes Windows client software, so you can easily set up a client to connect to your VPN. The downside, however, is that the NetMAX solution does come with per-client and per-server license fees. Legally, you can't buy one copy of NetMAX VPN server and install it on multiple machines, or install the client software on unlimited machines. Also there is no Linux client software, so if some of your road warriors are on Linux machines you'll still have to hand-configure those clients.

On the other hand, the NetMAX software is very easy to use and is fairly reasonably priced compared to other proprietary solutions. It might be worthwhile to look into if you're going to be setting up several VPNs—or just one in a hurry.