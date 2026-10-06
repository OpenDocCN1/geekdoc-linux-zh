
# Chapter 5 ♦ Getting on the Internet 187

5. If you are able to reach an IP address on your LAN with ping, but are unable to ping a computer by name, you may not be communicating with your DNS server. Repeat the ping command with the IP address of your DNS server to see if it is up and that you are able to communicate with it.

6. Check your DHCP information. If you obtained your IP address from a DHCP server, chances that your DHCP server led you other information you need to use the network as well. Look for a file that contains information about your DHCP lease. The lease includes information about the address that has been assigned to you, as well as how long you can keep it. In Fedora, lease information is held in the /var/lib/dhcp-client-eth0.leases file. Here's an example of information from that:

```
lease {
    interface eth0;
    fixed-address 10.0.0.204;
    option subnet-mask 255.255.255.0;
    option routers 10.0.0.1;
    option dhcp-lease-time 21600;
    option dhcp-message-type 5;
    option domain-name-servers 10.0.0.2;
    option domain-name-servers 10.0.0.3;
    option dhcp-server-identifier 10.0.0.5;
    option domain-name "linuxtrouble.com";
    renew 2005/07/21 01:23:06;
    rebind 2005/07/21 04:22:48;
    expire 2005/07/21 05:07:48;
}
```

Here you can see that the IP address assigned to the machine is 10.0.0.204, with a subnet mask of 255.255.255.0. The machine acting as the router to the Internet (also the gateway) is 10.0.0.1. The DNS servers are 10.0.0.2 and 10.0.0.3 (you can ping those numbers to see if you can reach your DNS servers).

## Dial-up Connections to the Internet

Many individuals and even small businesses that need to connect to the Internet still do use modems and telephone lines. The modem connects to a serial port (COM1, COM2, and so on) on your computer and then into a phone jack. Your computer dials a modem at your Internet service provider or business that has a connection to the Internet.

The most common protocol for making dial-up connections to the Internet (or other TCP/IP network) is Point-to-Point Protocol (PPP). Let's look at how to use PPP to connect to the Internet.

![](img/a2d958d7eab32ca5b89b2b8af808aa70_218_0.png)

See Chapter 9 for information on configuring a dial-up connection that is for Debian.

## Getting Information

To establish a PPP connection, you need to get some information from the administrator of the network you are connecting to. This is either your Internet provider (ISP) when you sign up for Internet service, or the person in your workplace who walks around carrying cables, two or more cellular phones, and a couple of beepers (when a network goes down, these people are in demand!). Here is the kind of information you need to set up your PPP connection:

- Account name and password— Used to verify that you have an Internet account with the ISP. This is an account when you connect to Linux or other UNIX system, may be referred to as a system name when you connect to NT server.
- An IP number— Most ISPs use Dynamic IP numbers, which means that you are assigned an IP number temporarily when you are connected. Your ISP assigns a permanent number if it uses Static IP addresses. If your computer or all the computers on your LAN need to have a more permanent permanence on the network, you may be given one Static IP number or a set of Static IP addresses.
- DNS Server addresses— Your computer translates host names to IP addresses by querying a domain name (DNS) server. Your ISP should give you at least one IP address for a preferred (and possibly alternate) DNS server.
- PAP or CHAP secrets— You may need a PAP (Password Authentication Protocol) or CHAP (Challenge Handshake Authentication Protocol) ID or a secret, instead of a username and password when connecting to a Windows NT system. These features are used with authentication on Microsoft and some other operating systems. Linux and other UNIX systems don't typically use this type of authentication, although they support PAP and CHAP on the client side. Your ISP will tell you if you are using PAP or CHAP.

Your ISP typically provides services such as news and mail servers for use with your Internet connection. To configure these useful services, you need the following information:

- Mail server— If your ISP provides you with an e-mail account, you will know the type of the mail server, the type of mail service (such as POP3— Post Office Protocol, or IMAP—Internet Access Protocol), and the authentication password for the mail server so you can get your e-mail.
- News server— If your ISP provides the name of a news server so that you can participate in newsgroups, the server may require you to log on, so you will need a password. The ISP provides that password, if required.

After you've gathered this information, you're ready to set up the modem.

## Setting Up Dial-Up

PPP is used to create connections. Before you begin, physically connect your modem to your computer. If you have an internal modem, check the telephone port on the back of your computer.

To simplify the process, many Linux systems use the Internet Configuration Wizard. For example, from the main desktop, choose Options ← Internet Configuration. The Select Device window appears.

The rate at which the computer talks to the modem is typically faster than the modem can talk over the phone lines. The default is 11520 bits per second, which is properly fine for dial-up.

Two tools are the following:

### Creating a Dial-Up Connection with the Internet Configuration Wizard

If you are using a Fedora or RHEL system, you can use the Internet Configuration Wizard. Here's how:

1. Choose Options ← Internet Configuration from the main menu. (Type the root password, if prompted.) A Select Device window appears (see Figure 5-7).
2. Select Modem and click Forward. The wizard searches for a modem and then the Select Modem window appears.
3. Select the following modem properties:

- Modem Device— If the modem is connected to your first serial port (COM1) you can select /dev/ttyS0; for the second serial port (COM2) choose /dev/ttyS1. (By convention, the device is linked to /dev/modem. Type Is - /dev/modem to see if it is linked to /dev/ttyS0 or another tty device.)
- Baud Rate— (Default)
- Flow Control— Check the modem documentation to see if the modem supports hardware control (CRCTS). If it doesn't, select software flow control (XON/XOFF).
- Modem Volume— This is off by default
- Use Touch Tone Dialing— Leave this check box selected in most cases. If for some reason your phone system doesn't support touch-tone dialing, you can turn it off.

![](img/a2d958d7eab32ca5b89b2b8af808aa70_221_0.png)

Figure 5-7: The Internet Configuration Wizard helps you set a PPP connection.
