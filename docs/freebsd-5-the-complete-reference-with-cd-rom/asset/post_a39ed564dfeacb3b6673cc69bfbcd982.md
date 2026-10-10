
## What Is PPPoE?

PPPoE is a way for broadband ISPs to assign IP addresses to customers' computers. In 2002, its use is restricted largely to low-end residential Digital Subscriber Line (DSL) accounts, although some business DSL accounts also use PPPoE. Cable modem ISPs generally use DHCP for IP address assignment, and high-end DSL accounts typically use static IP address assignment. PPPoE is a way to use Ethernet as a medium for PPP encapsulation, rather than the more common RS-232 serial line.

Why use PPPoE, though? After all, TCP/IP has been working directly on Ethernet for a long time, so PPPoE complicates matters by adding an extra layer to the Internet connection. The short answer is that PPPoE makes life easier for ISPs, by providing tools that help them manage IP addresses and monitor account usage. PPPoE offers few benefits to subscribers; however, you may have no choice but to use it with some ISPs.

## PPPoE Packages for FreeBSD

Two common approaches to using PPPoE with FreeBSD are:

- **User-mode PPP**: The same tool that provides user-mode PPP support over RS-232 serial ports also supports PPPoE. (This program is not the same as the kernel PPP daemon described in the earlier section, "Configuring Kernel PPP.")
- **Roaring Penguin**: The Roaring Penguin package (http://www.roaringpenguin.com/PPPoE/) provides an alternative that originated in the Linux world, but is available through the FreeBSD ports system. Roaring Penguin has the advantage of offering a GUI interface.

The next section, "Configuring PPPoE," describes the standard FreeBSD user-mode PPP tool as applied to PPPoE.

## Configuring PPPoE

The main feature you need to adjust to get PPPoE working is the `/etc/ppp/ppp.conf` file. Listing 15-3 shows a typical `ppp.conf` file configured for PPPoE.

### Listing 15-3. Sample /etc/ppp/ppp.conf File for Use with PPPoE

```
default:
    set log Phase tun command
    set ifaddr 10.0.0.1/0 10.0.0.2/0

broadband_isp_name:
    set device PPPoE:fxp0
    set authname agb
    set authkey w8tS4nr6
    set dial
    set login
    add default HISADDR
```

Several of the options in Listing 15-3 require explanation or customization:

- `broadband_isp_name`: This line contains the name of your configuration. It’s common to name it after your ISP. If you want to use ppp to initiate both broadband and conventional telephone modem PPP connections, you can create another section for the conventional telephone modem connection. (The default ppp.conf file includes such a section, called papchap.)
- `set device PPPoE:fxp0`: This option tells ppp that you’ll be using PPPoE, and identifies your Ethernet device. Change fxp0 to whatever’s appropriate for your network hardware. (Type ifconfig to see a list of your network devices. Chapter 14 describes identifying your Ethernet device in more detail.) Some ISPs require the use of a service tag, which is a name that identifies a particular PPPoE server. If your ISP has given you one, include it after the Ethernet device name and a colon, as in `set device PPPoE:fxp0:service_tag`.
- **Username and password**: The `set authname` and `set authkey` lines set your username and password, as assigned by your ISP. They’re set to `agb` and `w8tS4nr6`, respectively, in Listing 15-3.
- **Default route**: The `add default HISADDR` line tells ppp to add a default route for the connection. If by some chance the PPPoE line connection is a secondary link, you may want to omit this line, but for most configurations, you should leave it.

## Using PPPoE

Once PPPoE is configured, you can use it by typing the command:

```
# ppp -d dial broadband_isp_name
```

Naturally, you must change `broadband_isp_name` as appropriate. At this point, ppp “dials” your ISP. The system initiates a PPPoE discovery and connection process to link up to your ISP’s PPPoE server. If all goes well, you’ll then be able to use your PPPoE connection as you would any other Internet connection. You can do basic tests with ping, use mail clients, and so on. As with a pppd-based serial-line PPP connection, you terminate a PPPoE connection by killing the process that initiated it:

```
# killall ppp
```

If you want FreeBSD to bring up the PPPoE interface whenever it boots, you should add the following lines to `/etc/rc.conf`:

```text
ppp_enable="YES"
ppp_mode="ddial"
ppp_nat="NO"
ppp_profile="broadband_isp_name"
```

Once again, replace `broadband_isp_name` with whatever you called the configuration in your `/etc/ppp/ppp.conf` file. Also, if you want your FreeBSD system to function as a router that implements Network Address Translation (NAT) for other systems on your network, change `ppp_nat="NO"` to `ppp_nat="YES"`. A NAT router enables many computers to share a single external IP address—the broadband routers mentioned earlier, in "Using PPPoE with DSL," implement NAT. (Chapter 17 describes NAT routing in more detail.)

## Summary

Most computers today are networked. FreeBSD systems are frequently linked to the Internet via permanent network connections, as described in Chapter 14; however, dial-up telephone links remain important for many individuals and small businesses. These connections are usually implemented using a protocol known as PPP, and FreeBSD supports PPP. Dial-up links can be initiated through GUI tools such as X-ISP or through text-mode programs such as pppd. One variant of PPP that's growing in importance is PPPoE, which works over Ethernet rather than over RS-232 serial or modem lines. Many low-end DSL providers use PPPoE. You can configure FreeBSD to support PPPoE using the ppp tool or the Roaring Penguin PPPoE client.

# The Complete Reference

![](img/f34d37e3abe9f4517128e54f80ab2616_432_0.png)

# Chapter 16

# Principles of Network Clients and Servers

## Understanding the Roles of Clients and Servers

In any network transaction, just as in any human conversation, one party must “talk” first. In networking, that party is the client. The client requests a data transfer with the server. Typically, both the client and server transfer many data packets in the subsequent exchange, or even in the Prelude to the main transfer, such as in authentication procedures, preliminaries required to establish a secure encrypted connection, and so on. Often, the main transfer is of a file, such as a file transferred via FTP or a web page. Free e-mail messages are stored as files on the client or server. Sometimes, the main transfer isn’t a complete file. For instance, DNS lookups involve the transfer of just a few pieces of information from much larger files; and remote login sessions transfer information that the user types and programs’ output.

The bulk of the data transfer may go in either direction. For instance, in a typical web browser session, the browser (the client) requests that the server send files, so most data travels from the server to the client. This isn’t always the case, though; for instance, an FTP user can upload files from the client to the server, and in a Simple Mail Transfer Protocol (SMTP) mail session, the mail is sent from the client to the server.

Both the terms *client* and *server* may apply to either individual programs or to the computers that run those programs. It’s usually clear from context which meaning is intended. In this book, I elaborate by using a phrase such as “the server computer” when this might not be the case and the distinction is important. The terms are often clearest in the sense of server programs because an individual computer can run both client and server programs. For instance, a computer might run a Telnet server to enable people to use it remotely, and this same system might also host mail client programs. Such a computer functions as both a client and a server. Indeed, a few programs can assume both roles. For instance, SMTP mail servers often relay mail to other mail servers. Such a program acts as a server when it receives mail, but takes on the client role when it sends the mail to another system. Such programs are generally referred to as servers, despite their dual roles.

Many people think of servers as mysterious and powerful computers that reside in locked rooms, and clients as computers at which individuals sit. This conception is usually not far wrong, but it’s not part of the definition of clients and servers, which
