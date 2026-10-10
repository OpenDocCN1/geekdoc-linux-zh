
I wrote this chapter in response to several readers of earlier editions of this book who wanted to replace their Windows servers with Linux servers. I hope this chapter will help start them, and you, on the road to taking full advantage of powerful networked Linux features from your easy-to-use Mac desktops.

## Looking Inside Mac OS X

Inside Apple computers for the past few years is an operating system referred to as *Mac OS X*. You might also hear Mac OS X referred to as *Jaguar*, *Panther*, or *Tiger* (or *Leopard*, which was released in October, 2007). As with Linux, OS X has a free UNIX-like operating system at its core that, in this case, has been turned into a commercial product. That core, instead of being a Linux kernel, was originally based on a BSD-derivative open source project called Darwin (*www.opendarwin.org*).

Although Mac OS X and Linux are very different on the surface, there are many *striking* similarities. If you open a Terminal (shell) window on your Mac, you'll find that you can use many of the same basic commands that you can use from Linux. In addition, many of the same open source projects are included in both operating systems. These include:

- Samba (Windows file/printer server)
- Apache (Web server)
- CUPS (Linux print service)
- Sendmail (mail transport agent)
- BIND (DNS server)

There are also a few differences:

- Fedora is primarily covered under the General Public License, while OS X is based partly on an Open Source license and partly on a proprietary license. In August, 2003, the Apple Public Source License (APSL 2.0) was released (*www.opensource.apple.com/apsl*) and is now certified as a Free Software License from the Free Software Foundation.
- Fedora uses the Linux kernel; Mac OS X is based on a Mach micro-kernel surrounded by FreeBSD services. (Apple refers to this kernel as XNU and released it as a component of the Darwin open source operating system.)
- Most configuration in Fedora and RHEL is done using system-config windows, which often create text-based configuration files (mostly in the /etc directory) from command-line or GUI applications; Mac OS X stores the configuration file in its own NetInfo database, which is manipulated primarily by GUI tools as well as by the `niutil` command.

Fedora requires root permission for many administrative operations; OS X discourages overuse of the root login and encourages user accounts that are granted administrative privileges.

For the examples in this chapter, I originally used an iMac running Mac OS X 10.3.9 (Panther), although the later 10.4 (Tiger) is also available. For this latest edition of the book, I checked the text against Mac OS X version 10.4.8, running on an Intel-based Mac Mini. Because there were big improvements made after 10.1, I recommend that you upgrade your software if you are using 10.1. To see what version is installed on your Mac, choose About This Mac from the Apple menu on your Mac computer.

## Using Network Services from Mac OS X

You can easily connect your Mac OS X computer to your LAN by configuring the Network window. If Fedora or RHEL (or the equipment provided by your ISP) is configured as a DHCP server (see Chapter 23), your Mac OS X client can detect that. Or, you can configure your LAN interfaces manually, as follows:

1. From the Dock bar, click System Preferences and select Network. This opens the Network window, which enables you to configure your network interfaces.
2. If you are connecting to your Linux servers from a LAN, click the Show field and select Built-in Ethernet. The Network window appears, as shown in Figure 26-1.
3. Click the TCP/IP tab. Then select either DHCP or Manually in the Configure IPv4 field. If you select Manually, you can add the IP address of your computer, its netmask, the location of the router, the location of the DNS servers, and the domains to search. (For a home or small business, you might have a single Linux server serving as your router and DNS server. In this example, 10.0.0.1 is serving both of those functions.)
4. Click the AppleTalk tab. If you have configured your Linux server as an AppleTalk file and printer server (using netatalk), select the Make AppleTalk Active check box to turn on AppleTalk network protocols.
5. Click the Proxies tab. If you need to use a proxy server to access the Internet or other wide area network, use this tab to identify the proxies you are using.

The latest Mac computers have built-in Ethernet jacks that you can use to plug into your network switch or directly into your Internet hardware (such as DSL or cable modem). Plug your iMac into your network hardware and you should be ready to use your Linux servers from Mac OS X.

![](img/fb202c163797a743c3c6cf236316bc96_1013_0.png)

**Figure 26-1:** Configure your Mac OS X network interface to connect to Linux servers.

## Using AppleTalk (netatalk) from Mac OS X

AppleTalk is the traditional set of protocols used by Apple computers to share files and printers over a LAN. Although Mac OS X can support Samba file sharing, AppleTalk is still a familiar way for Mac users to get to networked printers and files.

Fedora and RHEL include a software package called netatalk that you can use to configure Linux as an AppleTalk file and printer server. To a Mac client, the netatalk server looks no different from any other AppleTalk server.

> **CROSS-REFERENCE:** Refer to the "Setting up the netatalk server" section later in this chapter.

To access a shared directory from an AppleTalk server, click Go in the Finder bar at the top of the screen, and then select Connect to Server. The Connect to Server window appears, as shown in Figure 26-2.

![](img/fb202c163797a743c3c6cf236316bc96_1014_0.png)

**Figure 26-2:** In Mac OS X, see Samba and AppleTalk shares from the Connect To Server window.

Enter the address, as shown in Figure 26-2, or click the Browse button to see a list of available servers.

After you click Connect, a pop-up window appears, prompting for a user name and password. Use the Options window to set up your preferences for logging on to the server. You can have the password added to your keychain so you don't have to type it in each time you access the server.

From the Options window, you can also select to send the password in clear text (which is the default) and be warned that you are doing that. The server determines whether you need to enter a clear-text or encrypted password (so if you send the wrong type of password, it will fail). You can also request a secure connection over SSH (which is a good idea to prevent someone from sniffing out your password from the network).

Figure 26-3 shows the Options window for selecting password options as just described.

![](img/fb202c163797a743c3c6cf236316bc96_1014_1.png)

**Figure 26-3:** Select authentication options when you connect to your AppleTalk (netatalk) server.

After the user name and password are accepted, an icon representing the AppleTalk share appears on your desktop. Double-click to open the shared directory. You can change the contents of that directory in any way that your login allows.

### Using AppleTalk from Mac OS 8 or OS 9

Prior to Mac OS X, Mac clients accessed AppleTalk shares from the Chooser window. The procedure for accessing a netatalk (or other AppleTalk) server went something like this:

1. Click the Apple menu and select Chooser. The Chooser window appears.
2. Click AppleShare. The file servers available on the local network appear in the Select a File Server window.
3. Click the file server you want to access and click OK. You are prompted for a user name and password (or just presented with a guest login).
4. Add the requested information and click OK. An icon representing the server appears on the desktop.

At this point, you can open the icon representing the shared directories and begin using the files and subfolders contained within.

### Using Mac, Windows, and Linux servers (Samba)

The procedure for accessing Samba servers from your Mac OS X system is similar to the procedure for accessing an AppleTalk server from Mac OS X. As with the AppleTalk procedure, you open the Go menu from the Finder bar and select Connect to Server. From the Connect to Server window, do the following:

1. Click the Browse button, and then click the workgroup name that contains the Samba server that you want.

> **TIP:** If you're not sure if the server is a Samba or AppleTalk server, look at the address at the bottom of the window after you click the server name. A Samba (SMB) address begins with `smb://`, while an AppleTalk server begins with `afp://`.

2. Choose the server you want to open and double-click it. You will likely be prompted for your Samba user name and password from the SMB/CIFS FileSystem Authentication window (see Figure 26-4).
