
Software modems are available as internal models only. The computations required to implement a software modem require the high speed of an ISA or PCI slot. You can usually identify a software modem by checking the requirements panel on the modem's box. If it lists a Pentium CPU or Windows among its minimum requirements, it's almost certainly a software modem. If the box lists an 80486 or earlier CPU, or DOS, OS/2, or Linux among its minimum requirements, chances are it's a controller-based modem. (If the box lists a Pentium CPU and mentions Linux but not DOS, it might be a software modem for which Linux drivers are available.) External modems are almost always Linux compatible. The main exceptions are some USB modems. As described in the sidebar, “USB Modems,” earlier in this chapter, some of these devices work with Linux's USB drivers, but some don't.

If you have a software modem, you might as well look for Linux drivers before you attempt to replace it. The Web site http://www.l1nmodems.org has the latest information on software modems under Linux, including links to drivers, information on software modem chipsets, and miscellaneous additional information.

> **NOTE**
> A few internal modems have been released based on IBM Mwave chips. These products usually support both modem and sound card functionality. They aren't software modems in the same sense as are most software modems, because the Mwave chip performs the usual modem processing functions. Mwave products do rely upon specialized drivers to load the modem processing code, however, and so don't work under Linux. There have been some abortive attempts to write Linux drivers for Mwave devices, but none has yet borne fruit.

## Extra Modem Features

All modems sold today support conventional data traffic using the v.90 protocol (or possibly only some earlier protocol, if it's an older model in a closout bin). Additional features supported by anywhere from a few to the vast majority of modems include:

-   **K56Flex**: K56Flex was a 56Kbps modem protocol that predated v.90. It was used by a variety of modem manufacturers, led by the modem chipset manufacturer Rockwell. Some ISPs still support K56Flex, but I don't recommend buying a K56Flex modem unless it also supports v.90.
-   **x2**: Like K56Flex, x2 was a 56Kbps protocol that predated v.90. This protocol was used mostly in U.S. Robotics (USR) modems (USR has since been bought by 3Com). As with K56Flex, I only recommend buying an x2 modem if it also supports v.90.
-   **Fax features**: The capability to both send and receive faxes is standard on modern modems. As a general rule, you should look for a modem that supports Class 2.0 fax protocols, which impose the least overhead on the sending applications. In Linux, programs such as `mgetty+sendfax` (`http://alpha.greenie.net/mgetty/`) or HylaFax (`http://www.hylafax.org/`) handle sending and receiving faxes. Unfortunately, most of these programs are far less user-friendly than are their Windows equivalents. Matters are improved somewhat by fax front-end programs like GFax (`http://www.gmsys.com/gnome-gfax.html`), which provide an easy-to-use GUI atop the underlying fax software.
-   **Voice features**: Some modems support voice functionality. You can use these modems as speakerphones, answering machines, or voicemail systems. Linux support for these devices exists, but is extremely crude compared to the user-friendly Windows voicemail programs for the same hardware. The main Linux package for voice modems is `vgetty` (`http://alpha.greenie.net/vgetty/index.html`). This is a variant of the `mgetty+sendfax` package.

### Using Modems for PPP Internet Connections

You can use a modem to connect your Linux computer to the Internet using the *Point-to-Point Protocol* (PPP). Most Linux distributions today include tools to help you manage a PPP dial-up account. For instance, the *K Desktop Environment* (KDE), which is the default desktop on many Linux installations, includes a program called *kppp*, shown in Figure 18.3. When you click the Setup button in the main window, you get the *kppp Configuration* window shown in the foreground. You can enter information on your PPP account in this window much as you would enter information in a Windows PPP dialer: When you're done, you can connect to your ISP by clicking the Connect button in the main *kppp* window. Other GUI PPP dialers function in a similar fashion, although the details differ.

Depending upon the authentication method you use, you might need to take one additional step: You might need to add your username and password to the `/etc/ppp/pap-secrets` or `/etc/ppp/chap-secrets` file, depending upon whether your ISP uses PAP or CHAP authentication. These files are readable only by *root*, and they contain your sensitive passwords. An example is

```
# client  server secret    IP addresses
rootsmith *   password
```

This sample file allows the user *rootsmith* to log in to a PPP server using the password *password*. In most cases you want to leave the *server* field set to an asterisk (*), which allows a login to any server. If you're assigned a static IP address by your ISP, you can enter it in the final IP addresses field; otherwise, leave that field blank.

![](img/860d0c38bd76c9ded976e9d1e179ef25_516_0.png)

**FIGURE 18.3**  
The kppp program is a typical PPP GUI dial-up utility.

## Null Modem Cables

Sometimes you need to connect two computers together via their serial or parallel ports. This can be an inexpensive way to network the two computers, or it can be a way to use one computer as an inexpensive terminal for another. For instance, you can use an old 8088 computer as a terminal for a much more capable Linux box. This can be a good way to use Linux’s multiuser capabilities. Precisely how you make these connections depends on whether you want to use a serial or parallel port for this purpose.

### Serial Null Modem Cables

The easiest way to use a serial port for connecting two computers is to purchase a *null modem* cable or an adapter to turn a conventional modem cable into a null modem cable. Figure 18.4 shows both a null modem cable and a null modem adapter. The null modem cable closely resembles an ordinary RS-232 serial cable, except that both connectors are female, which is unusual in conventional modem cables. For modern x86 computers, both ends use 9-pin connectors, but if you want to link a computer that uses a 25-pin serial connector, one or both ends might need to have 25 pins.

![](img/860d0c38bd76c9ded976e9d1e179ef25_517_0.png)

**FIGURE 18.4**

Null modem cables look very much like ordinary cables, so I recommend you label them as null modem devices, if they aren’t so labeled when you buy them.

> **NOTE**
> You might occasionally run into a serial null modem cable on which one end uses a specialized connector. For instance, cables of this sort come with many palmtop computers. You can use these cables to link the palmtop to your Linux computer, and then use the Linux computer via a terminal program or a PPP link.

Precisely how you configure your Linux computer to work with the null modem cable depends on what you want to do with it. In most cases, you must modify the `/etc/inittab` file. This file should have a number of lines that look something like this:

```
# Run gettys in standard runlevels
1:12345:respawn:/sbin/getty tty1 VC linux
2:12345:respawn:/sbin/getty tty2 VC linux
3:2345:respawn:/sbin/getty tty3 VC linux
4:2345:respawn:/sbin/getty tty4 VC linux
5:2345:respawn:/sbin/getty tty5 VC linux
6:2345:respawn:/sbin/getty tty6 VC linux
```

These lines run the `getty` program, which handles the text-mode `login:` prompt. Each instance of `getty` in the preceding example is linked to a different `linux virtual console`, identified by the `ttyN` number on each line. You should add a similar line for any additional function you want to perform with the serial port. For instance, if you want to use another computer as a *dumb terminal*, which provides only text-mode access, you could add a line like the following:

`S0:2345:respawn:/sbin/getty ttyS0 VC linux`

This line allows for a 19,200 bps connection to `/dev/ttyS0` via a null modem cable. The computer you use as a dumb terminal could be an old-style terminal (such as a DEC VT-100) or it could be a PC, Macintosh, palmtop, or some other system running a terminal program.

![](img/860d0c38bd76c9ded976e9d1e179ef25_518_0.png)

Linux distributions differ in the details of how they provide login access. Specifically, there are several serial variants on the `getty` program, such as `getty`, `mingetty`, and `mgetty`. Each of these programs has different capabilities. For instance, `mingetty` can't handle serial port access, so if your distribution uses `mingetty`, you might need to use `getty` or `mgetty` instead of `mingetty` to use a terminal connected to a serial port with Linux. You can continue using `mingetty` on the virtual console devices.

In some cases, you might need to replace the call to `/sbin/getty` with a call to some other program. For instance, if you want to use the serial port for a PPP connection, you would use `pppd` in place of `getty`. You can also use more advanced `getty`-like programs, such as `mgetty`, to handle real modems for dial-in access or fax reception.

For the most part, serial ports aren't a very efficient communication method. The maximum serial port speed of 115Kbps is simply too low compared to the speeds that are possible with Ethernet (10~100Mbps) or other networking technologies. Therefore, serial ports aren't much used for serious networking. They can be very useful for limited text-mode logins, though.

## PLIP for Parallel-Port Networking

Parallel ports, like serial ports, can be used with a sort of null modem cable. The term *null modem cable* isn't generally used in reference to parallel ports, however. Under Linux, the primary use of parallel-port, computer-to-computer communication is as a low-cost network interface. Because every x86 computer manufactured in recent years has a parallel port, you can connect any two arbitrary computers without adding additional hardware to either computer. You do need a special parallel cable, however.
