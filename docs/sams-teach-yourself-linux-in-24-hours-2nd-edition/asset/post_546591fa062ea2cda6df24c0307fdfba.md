
![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_244_0.png)

## Hour 10
### Connecting to the Internet

In this hour, you'll learn how to set up your Linux system to connect to the Internet using the serial line Point-to-Point Protocol known as PPP. Connecting to the Internet is one of the biggest hurdles many new OpenLinux users face after installing OpenLinux, configuring OpenLinux to work with their computer's sound card, and configuring the X Window System to work with their computer's graphics card. After following the directions in this lesson, you can connect to the Internet through your Internet Service Provider (ISP), and do email, Web browsing, and file transfers.

This hour shows you how to connect to your ISP manually in the simplest, most basic way possible. I also point you to sources of information for more details so that you can troubleshoot or fine-tune your connection. You'll then learn how to use two easy-to-use graphical interface programs, kppp and xisp, to set up, start, and stop your PPP connection.

I'm recommending you use a PPP connection for a number of reasons:

- Although it's complex, it is easy to set up.
- You can find documentation and details on the protocol in a number of HOWTO documents.
- You can read the comp.protocols.ppp newsgroup about PPP and the comp.os.linux.networking newsgroup for specific Linux information.
- It offers security on both ends of the connection.
- It is a common protocol supported by nearly all ISPs.
- OpenLinux comes with several programs you can use to set up your PPP connection.
- It is flexible enough to accommodate different types of connections.

This hour starts by listing some of the hardware and software prerequisites for OpenLinux and then asks for some necessary information you need from your ISP. Using that information, you'll first create a set of customized scripts you can use to manually start or stop your connection. I'll then show you how to set up a PPP connection using two graphical interface programs: the kppp client for the K Desktop Environment and the xisp graphical interface client for X11.

You'll also learn about some handy utilities you can use to diagnose your connection and some other programs you can use to monitor your sessions.

### Hardware You Need

You probably already have all the hardware you need: a modem, a modem cable if your modem is external, and a phone line. However, you must have a modem you can use with OpenLinux. You cannot use any of the following modems with OpenLinux:

- 3Com/U.S. Robotics 56K V.90 Winmodem
- 3Com/U.S. Robotics 56K Winmodem PC Card
- 3Com/U.S. Robotics Sportster 33.6 Winmodem
- Aztech Systems 56K PCI modem
- Cardinal 56K Windows Fax modem
- Diamond SupraMax 56K ISA/PCI modems
- Hayes 56K Accura V.90 PCI Win modem
- Motorola FM56 ISA/PCI modems
- Mwave adapters (but might work as sound card)
- Viking Components 56K ISA Windows modem
- WinStorm 56K PCI Data/Fax Speaker phone modem
- Zoltrix Phantom/Spirit 56K modems
- Any other modem requiring Windows-only software

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_246_0.png)

> If you plan to purchase a modem to use with OpenLinux, do not buy any modem considered a winmodem. These useless pieces of junk were recently introduced into the computer industry by manufacturers to save money and increase profits in hardware production. Winmodems use fewer chips than "real" modems and depend on operating system-specific software drivers (and your computer's CPU) in order to work. Unfortunately, many computer manufacturers (especially those that make and sell laptop computers) do not tell you that a provided or built-in modem does not work with any operating system other than Windows. Beware! If you're not sure about what modem to buy, get an external modem that works with any operating system, not just Windows.

One of the great things about OpenLinux is that it runs well even on older computers. Although graphics-intensive applications such as X can tax the capabilities of older, slower PCs, you don't need X11, a fancy display monitor, or a 16MB VRAM accelerated 3D video card to use PPP. You do, however, need a working serial port and modem.

If you're able to use your modem under Linux to dial out and connect using the minicom program or C-Kermit, chances are you won't have any problems. If you're using a laptop with a PC Card modem and the cardmgr PCMCIA device manager recognizes and initializes your modem, you should be okay, as any recognized card is identified and listed when you boot OpenLinux.

One way to check for serial-port recognition is to use the dmesg program, which displays the boot messages shown when you start OpenLinux. Run the dmesg program (piped through the less command), and look for lines in the output describing serial ports similar to these:

```
# dmesg | less
...
ttyS0 at 0x03f8 (irq = 4) is a 16550A
ttyS1 at 0x02f8 (irq = 5) is a 16550A
ttyS3 at 0x02e8 (irq = 3) is a 16550A
...
```

Using dmesg is convenient, especially if the boot messages scroll by too fast for you to read. These lines show that three serial ports were found using the devices ttyS0, ttyS1, and ttyS3. Another consideration is your modem's speed. You might remember when 2400- or 9600-baud modems were the greatest innovation since touch-tone dialing. If you're still using an older modem and refuse to upgrade to the newer V.90 modems until model prices drop, you can still connect to the Internet with PPP; most older modems automatically synchronize with the newer models lodged in your ISP's modem bank.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_247_0.png)

> Want to lessen the chances of problems when connecting with your ISP? Find out what modems your ISP uses, and buy the same model for your computer system.

If you want to listen to radio stations, watch live video, or upgrade your Red Hat Linux system through your phone connection, you want the fastest modem and Internet connection you can afford. Although I don't advocate you try to get any work done through a 1200- or (shudder) 300-baud connection (which borders on masochism, but can be done, as ATM machines prove), you can use email, FTP, and text-only Web browsing at 9600 speeds.

It's up to you, and besides, isn't that what OpenLinux is all about—freedom of choice?

### Linux Software You Need

In order to set up your PPP connection, you need to make sure that your Linux kernel supports PPP. You might have PPP support compiled into the kernel or loaded as a module when you start Linux. One of the ways to check to see if PPP support exists on your system is to again use dmesg:

```
# dmesg | less
...
PPP: version 2.2.0 (dynamic channel allocation)
TCP compression code copyright 1989 Regents of the University of
California
PPP Dynamic channel allocation code copyright 1995 Caldera, Inc.
PPP line discipline registered.
...
```

You see similar lines.

> By default, OpenLinux loads PPP support via a loadable Linux kernel module. If you do not see PPP, you must either recompile the kernel with built-in PPP support, build the PPP module and use the insmod command to load the driver, or make sure you have selected the proper Linux kernel during your OpenLinux installation (with the word "modular" in its filename). You also need networking support enabled, especially TCP/IP. See Hour 2, "Installing Linux," for details.

You also need the chat program, found under the /usr/sbin directory, and part of the pppd daemon software package. The chat program is used during the dialing process to dial out and connect to your ISP's modem. Along with chat, you need the pppd daemon, also installed in the /usr/sbin directory. If pppd is installed, you can find a ppp directory under the /etc directory containing some or all of the following files:

```
# ls /etc/ppp
chap-secrets   options        ppp-on-dialer
connect-errors pap-secrets    ppp-on
ip-up          ppp-off
```

If you don't see the ppp-on or ppp-on-dialer files, you can copy them from the /usr/doc/ppp-2.2.0f directory.

The first setup you learn during this hour requires you to make changes to the ppp-on file, which is an executable script. Next, you might want to check to see if the file resolv.conf exists under the /etc directory. If it doesn't, don't worry; it's a short file containing one or two lines, and I show you what to type in the file.

Finally, you might want to see if you have the ifconfig, minicom, netstat, ping, and route commands on your system. You use these later in this chapter to run some tests on your connection.

> Need to look for a command? Try the whereis or locate commands like so: whereis ifconfig to see where the ifconfig command is located on your system or locate ifconfig to print a list of any files or directories using ifconfig.
