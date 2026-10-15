
## Virtual Private Networks

Another of the more advanced functions you can implement with Linux is a Virtual Private Network (VPN). VPNs are becoming a popular solution as security becomes more and more of an issue in information technology.

In this section we’ll look at a popular VPN solution for Linux and discuss one of the more popular commercial alternatives as well.

### PoPToP

If you’re looking to set up a VPN over PPTP with Linux, one of the tools you should take a look at is PoPToP. PoPToP is a PPTP implementation for Linux, and there are ports available for Solaris, OpenBSD, and FreeBSD—which might be of interest if you happen to be working in an environment with those operating systems in addition to Linux.

Because many commercial environments are a mixture of Linux servers and workstations with Windows clients, PoPToP supports Windows clients as well as Linux. So far, PoPToP supports Windows 95, 98, NT, and 2000. The price is also right, as PoPToP is licensed under the GNU General Public License—so no worries about license fees.

### Getting the Code

As of this writing, the most recent stable version of PoPToP is 1.0.1. There is also an unstable version with more cutting-edge features available, but we recommend you stick with the stable code unless there’s a feature that you desperately need in the development version, or if you want to assist with finding bugs and contributing code.

You can find PoPToP at http://poptop.1ineo.com/.

At the site you’ll find source code for Linux, Solaris, and other operating systems.

There are also RPMs compiled for i386 and source RPMs if you’re running a distribution that uses RPM. If you’ll be connecting from Windows clients, there are a few patches you’ll want to grab. To enable Microsoft Encryption (MPPE) or Microsoft Authentication (MSCHAPv2), you’ll need to download and install the appropriate patches, which are also available from the web site.

### Installing PoPToP

In this section we’ll show you how to install PoPToP on Linux from source. After you have the PoPToP code, cp it to the /tmp or /usr/local/src directory, depending on your personal preference.

Make sure that you’re logged in as root, uncompress the tarball that you retrieved, and then cd to the new directory. Then run

```
./configure
make
make install
```

Assuming there have been no compiler errors, you should now have the PoPToP binaries in /usr/local/bin. You also will need to be root to launch the PPTP daemon pptpd.

### Configuring and Debugging PoPToP

After everything has been compiled and installed, you'll need to edit three files to tweak everything for your installation. The files are /etc/pptpd.conf, /etc/ppp/chap-secrets, and /etc/ppp/options.

The /etc/ppp/chap-secrets is a text file containing the username, password, servername, and valid IP addresses that they can connect from. You'll want to add one or more users to this file so that they can connect to the server.

There is a sample /etc/pptpd.conf file included with the source download, which you can customize to your own tastes. You'll use this file to set the local and remote IP addresses, speed at which clients can connect, ports at which the daemon will listen, and debugging level. Make sure that you restart syslogd after starting pptpd to enable logging.

Finally, you'll need to edit /etc/ppp/options that is included with the source distribution to reflect the options in /etc/ppp/chap-secrets.

If you have any problems setting up PoPToP, you might want to check the PoPToP web site for troubleshooting tips or workarounds for particular clients. Right now there are several HOWTOs and setup guides for various Windows clients.

### Commercial VPN Solutions

If you're looking for a quick-and-easy solution to your routing and VPN needs, there are a few commercial solutions available that you might find easier to set up.

Most of these are based on the Open Source and Free Software tools but include slicker configuration tools. There are also some Linux-based hardware solutions that you might find to be interesting alternatives to Cisco routers.

### NetMAX VPN Server

One outstanding commercial product is the NetMAX VPN Server. It's a customized Linux distribution with web-based setup tools that allow you to quickly and easily set up an IPSec VPN solution. It also includes Windows client software, so you can easily set up a client to connect to your VPN. The downside, however, is that the NetMAX solution does come with per-client and per-server license fees. Legally, you can't buy one copy of NetMAX VPN server and install it on multiple machines, or install the client software on unlimited machines. Also there is no Linux client software, so if some of your road warriors are on Linux machines you'll still have to hand-configure those clients.

On the other hand, the NetMAX software is very easy to use and is fairly reasonably priced compared to other proprietary solutions. It might be worthwhile to look into if you're going to be setting up several VPNs—or just one in a hurry.
