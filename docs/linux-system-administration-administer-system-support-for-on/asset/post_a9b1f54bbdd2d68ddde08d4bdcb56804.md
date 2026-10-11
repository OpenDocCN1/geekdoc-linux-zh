
interfaces with modems. With dial-up connections, Slackware has two ways to interact: a terminal emulator or through network daemons pppd and slippd.

## Network Interface Cards

In the previous sections with setting up routing tables and Ethernet cards, this shows you how to manually set up a network interface card. However, you shouldn't need to do anything to set up the NIC if connecting through a kernel module or PCMCIA module. This should load the drivers and identify the card configurations as the information comes into the hardware.

## Terminal Emulation

If you want to have basic terminal emulation through a modem, you can use seyon, an X-based communication tool, and minicom, the non-X-window-based tool. Both do basically the same thing; they enable you to connect to another computer without having to set up an IP network connection. The difference between minicom and seyon is minicom is curses-based and seyon is X-based. Figure 11-10 illustrates seyon.

![](img/8ad518fddafc7f5e73715a2604b61d50_392_0.png)

To use the seyon or minicom program, first have handy the phone number you're connecting to, the login name, and the password. When you have this information, you can log in to your account and have access (similar to a telnet session, except through a modem).

To get started, press Ctrl-A and then Z on minicom. In seyon, a message will appear within the X window, prompting you for a number to dial.

## PPP

If you have an Internet Service provider, or want to connect to a network, you'll most likely use **PPP**. PPP is the Point-to-Point Protocol that enables you to dial directly into a server to access the resources on a network. This is the most commonly used connection via modem.

When you set up PPP, do so as root. Otherwise you can make your own work surprisingly difficult. You'll also want to double-check the permissions on network files. Make sure that everyone can read and execute them. An example of a good permission is **555** or **755**. If you don't have your permissions set properly, it may cause some weird problems when connecting. DNS has a tendency to cause problems with X and other networking software without meaning to. Always check your *`/etc/resolv.conf`* file. If you do have problems, you can always temporarily rename it to *`/etc/resolv.oid`*.

### SETTING UP PPP

Here are the basic steps for setting up PPP.

1. Run `/sbin/netconfig`. Follow the same directions as the `netconfig` command for setting up your network section.

2. Check your HOSTNAME file to make sure it's your username.domain.com. Your HOSTNAME file will be in the /etc directory.

For example, your screen should have something like this on it:

```
stripes:~# more /etc/HOSTNAME
stripes.nando.net
```

3. Check your `resolv.conf` file (in your `/etc` directory). The output should mirror the following:

```
stripes:~# more /etc/resolv.conf
domain best.com
nameserver 152.52.2.2
```

4. Type the following at your command prompt.

```
stripes:~# chmod 755 /etc/resolv.conf
stripes:~# chmod 755 /etc/HOSTNAME
```

This lets everyone read and execute the *`/etc/resolv.conf`* and *`/etc/HOSTNAME`* files. If you don't type these commands, you're going to be finding frustrating (I'm telling you this one from personal experience).

5. Check to be sure you have all your `ppp` files. They should be in the directory `/usr/lib/ppp`. Your directory listing should have these two files:

```
chat:
		ELF 32-bit LSB executable i386 (386 and up)
Version 1
pppd:
		ELF 32-bit LSB executable i386 (386 and up)
Version 1
```

### CONFIGURING PPP

Now, you're going to need to configure PPP. You'll need to run `/usr/sbin/`*`pppsetup`*. This section walks you through everything involved. When you enter the phone number, you'll need to enter your AT command before it so the modem recognizes it should dial. This is modem-specific (mine takes ATDT). Consult your modem manual for the specifics of your AT Commands.

For example, I would enter `ATDT8788888` to get it to dial. (See Figure 11-11.)

> The comma before the phone number means that the modem waits for another dial tone.

![](img/8ad518fddafc7f5e73715a2604b61d50_394_0.png)

If you disable call waiting, type the following:

```
ATDT*70,8788888
```

If you dial a nine before the number, type the following:

```
ATDT*9,8788888
```

Next you'll need to enter your modem device. Because mine is on serial port 1, my modem device is `/dev/cua0`. You also want to create a symbolic link from your actual modem, `/dev/cua[0-3]` to `/dev/modem`. The `seyon` program requires this, and it makes it easier for you to find your actual modem. Your cua, which is the modem serial device number, is one less than the COM port number. This number is determined the same way the serial mouse is. (See Figure 11-12.)

![](img/8ad518fddafc7f5e73715a2604b61d50_395_0.png)

Next, pick the baud rate (actually the kilobits-per-second speed) of your modem. The newer modems today are 56K, although you may be using something a bit slower (like 33.6, 28.8, or 14.4). (See Figure 11-13.)

![](img/8ad518fddafc7f5e73715a2604b61d50_395_1.png)

You'll need to know if your ISP has callback. Callback is a so-called security feature where the modem dials back your number to verify you're who you say you are. Most ISPs haven't enabled this. (See Figure 11-14.)

![](img/8ad518fddafc7f5e73715a2604b61d50_396_0.png)

Figure 11-14: Verifying callback information

The next question is authentication. If your ISP uses authentication, they probably use PAP. Some use CHAP, which encrypts the password you send them. PAP authenticates your password connection through cleartext, meaning your password is not encrypted. CHAP does the same thing that PAP does; additionally, it encrypts your password. (See Figure 11-15.)

You can run PPP as follows:

```
stripea:~# ppp-go
```

You don't have to stay in the root window to run since PPP runs from a daemon called pppd. The PPP daemon now controls all your network connections through the ISP and allows you to have Internet access. This is transparent to you, as you are using the ISP's resources (such as their nameserver and routers) to access the Internet. Just go to another window, run Netscape, telnet or ftp to other sites, and so on.

![](img/8ad518fddafc7f5e73715a2604b61d50_396_1.png)

Figure 11-15: PPP authentication

Disconnect *ppp* as follows:

```
striipes:~ ppp-off
ppp0 link terminated
```

## Other Networking Protocols

In addition to TCP/IP, you can use other protocols with Slackware Linux. They include Novell's addressing protocol IPX, Appletalk, and Microsoft's Netbios. There are applications out there to help you use these protocols like Samba for Netbios. These protocols enable Linux to communicate with many different computers using other network protocols.

### The IPX Protocol

Novell created the Internet Packet eXchange (IPX) protocol for hosts to communicate within a LAN. Novell built a suite of products that use IPX called Netware. IPX is still popular today, though the IP protocol is growing in implementation because of the Internet's popularity. However, many companies today still use IPX, and you can get Linux to work with IPX.

IPX uses the MAC address and the network address to create the host address. As a result, the addressing for IPX is cumbersome. For its configuration files, it uses the bindery. The bindery is a database of network configurations, including usernames, passwords, and routes. IPX can also share file systems over a network using the Netware Core Protocol, NCP. This works similarly to NFS on an IP network. Novell Directory Services (NDS) is used to provide information over a Novell network. Also, IPX uses Service Advertisement Protocol, SAP, to announce what services the host has to offer.

Linux can only run IPX over the network, not SAPs or NCP. For implementing IPX into your Linux host, you'll need to compile IPX into the kernel under Networking Options. If you want to get IPX tools, there are some available at ftp://sunsite.unc.edu/pub/linux/system/file system/tools/ ipx.tgz.

If you want to route IPX on your Linux host you can download the IPX RIP daemon at ftp://sunsite.unc.edu/pub/linux/system/file system/ tools/ ipxrpd-0.7.tgz. This will enable you to route IPX through your host.

Most recently, Caldera released a version of Unixware (Novell's implementation of Netware for UNIX) on Linux. You can find out more information about it at http://www.caldera.com.
