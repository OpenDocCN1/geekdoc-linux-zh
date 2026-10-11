
## Testing the Configuration

To make sure that both ends of the tunnel are configured correctly and that hosts on `leftsubnet` are indeed using the Denver-Boston tunnel to communicate with hosts on `rightsubnet`, issue the following commands on the DENVER gateway (for example):

```bash
[ramon]$ sudo ipsec auto --up denver-boston
[ramon]$ sudo ipsec auto --down denver-boston
[ramon]$ sudo ipsec look
```

After restarting the connection, the output of this last command should be similar to the following:

```text
athena.example.com Sun Feb 4 22:51:45 EST 2001
---------------------------
10.10.10.0/24 -> 10.20.20.0/24 => tun0
    x20
    0
5.55.76.10
->
esp
0
x
20
20
65.55.76.10
---------------------------
tun0
0
x
20
00
65.55.76.10 IPv4_Encapsulation: dir=out 65.66.67.10 ->
65.55.76.10
esp
0
x
20
30
65.66.67.10 3DES-MD5-96_Encryption: dir=in
iv=0
x
2 Cbca 5 ba4 2 ff bb seq=0 bit=0
x
000 000 00 win=0 flags=0
x
0
0>
esp
0
x
20
20
65.55.76.10 3DES-MD5-96_Encryption: dir=out
iv=0
x
2 Cbca 5 ba4 2 ff bb seq=0 bit=0
x
000 000 00 win=0 flags=0
x
0
0>

Destination Gateway Netmask Flags MSS Window irtt Iface
10.10.10.0 0.0.0.0 255.255.255.0 U 1500 0 0 eth1
10.20.20.0 65.55.76.10 255.255.255.0 UG 1404 0 0 ipsec0
```

If you see a similar report, your FreeS/WAN installation has been correctly configured.

## Point-to-Point Tunneling Protocol (PPTP)

The fact that IPsec is a standards-based framework developed under the auspices of the IETF has made it the most widely implemented VPN technology to date. In addition, since IPsec is a mandatory element of a standards-compliant IPv6 implementation, its popularity is only going to increase as the new IP version starts to gain momentum. But there are other competing protocols in the field of virtual private networking that have enjoyed some support from the Linux community. One of those is PPTP.

Developed under the auspices of the Microsoft Corporation, PPTP is an alternative to IPsec that was designed to provide a way to tunnel internal network packets out to remote office users using the Internet. PPTP uses the Point-to-Point Protocol (PPP) as the basis for tunneling, so all PPTP implementations rely on an existing (or bundled) PPP installation. While PPTP is primarily a packet encapsulation standard, it includes provisions to add connection security in two areas:

- **Authentication**: PPTP uses the authentication methods typically supported by PPP devices, both Microsoft and third-party devices such as PAP (Password Authentication Protocol), which is actually not secure at all, and CHAP (Challenge Handshake Authentication Protocol), including its Microsoft and Shiva variants.
- **Privacy**: Microsoft defined an optional encryption protocol to be used to protect the privacy of PPTP packet payload as it traverses an untrusted network. The Microsoft Point-to-Point Encryption (MPPE) protocol uses the RC4 encryption algorithm with the password as the seed to generate session keys for encryption.

A PPTP client (typically a Windows laptop or home user) works directly with the PPTP server at the edge of the corporate LAN, as illustrated in Figure 12.9.

![Figure 12.9](img/3258bbaf790525f8c4eb25fabff7844a_379_0.png)

Once the PPTP client has established IP connectivity, typically over PPP to the ISP's nearest remote access server (RAS), it uses PPTP messages (which run on top of TCP) to establish a connection to the PPTP server and negotiate a set of tunnel addresses. The PPP process at the PPTP server assigns both a local and a remote address for the resulting PPP tunnel. After the user has authenticated successfully, a Generic Routing Encapsulation (GRE) session is built from end to end that sustains the PPP connection just negotiated. Only after these steps have taken place can both peers start exchanging IP packets. Note that the addresses of the PPP-encapsulated IP packets are negotiated by the two endpoints and do not have to be legal Internet addresses.

> **NOTE**: While the PPTP specification is solid overall, Microsoft's implementation has come under scrutiny over the last few years. Some improvements have been made, but I recommend that you take a quick look at http://www.counterpane.com/ppp-faq.html for more information on this controversy.

While Microsoft bundles both a client and a server implementation in its Windows platforms, there is an open-source PPTP server for Linux that can interoperate with the Windows-supplied clients. This implementation, called PopTop, is discussed in the next section.

## PopTop

PopTop is an implementation of the PPTP protocol that includes a Linux port, as well as many other UNIX variants. It consists of

- A simple daemon (`pptpd`)
- A configuration file named `/etc/pptpd.conf`
- A set of man pages and supporting documentation.

PopTop is interoperable with Microsoft Windows 95, 98, NT, and 2000 clients. Its home page can be found at http://pptop.linux.com, and a well-frequented mailing list can be accessed by subscribing at that Web site.

### Downloading PopTop

PopTop is available on most repositories of RPM format packages. Simply download the latest distribution and install as follows:

```bash
[ramon]$ sudo rpm -i pptpd-1.1.1-1.i686.rpm
```

You'll see the main PPTP daemon executable in `/usr/sbin/pptpd` and a sample configuration file in `/etc/pptpd.conf`.

To make sure you have PPP installed (you'll need version 2.3.5 or later), execute the following command:

```bash
[ramon]$ rpm -q ppp
ppp-2.3.11-7
```

### Configuring PopTop

Let's start by configuring the PPP layer. Edit the `/etc/ppp/options` file and make sure that it contains the following options:

- `name athena`: This is the name of the local system.
- `auth`: This option requires the peer to authenticate itself.
- `require-chap`: This option specifies to only accept CHAP authentication.
- `proxyarp`: This option adds an entry to this system's ARP (Address Resolution Protocol) table with the IP address of the peer and the Ethernet address of this system.

The `require-chap` setting ensures that PPP requires the remote end to authenticate itself using the CHAP algorithm. Avoid using PAP because it sends the username and password in the clear (unencrypted or unhashed). In addition, the `proxyarp` setting specifies that the PPTP server listen for proxy requests for the remote user and forward packets to them accordingly.

You should also set up some basic authentication. Let's start by creating some entries in `/etc/ppp/chap-secrets` of the following form:

```text
alice athena     'alicepassWord'      10.20.20.100
bob   athena     'bobpassWord'        10.20.20.101
charlie athena   'charliepassWord'    10.20.20.102
```

Using these settings, you will now accept CHAP authentication requests for alice, with password `alicepassWord`. The second field is simply a reference to the local server (athena). The fourth field contains the IP address that will be assigned to the user's end of the PPP connection.

Finally, create the `/etc/pptpd.conf` file and insert the following sample values:

```text
localip 192.168.1.1
remoteip 10.20.20.100-254
```

The `localip` value can be the same for all connections; it is simply the local end of the PPP tunnel established to support all incoming PPTP connections. While the local end can be common, there is a requirement that the remote end be uniquely addressed. The `remoteip` line specifies the range of IP addresses that incoming clients will use for that purpose.

> **NOTE**: If you do not allow a large enough `remoteip` range to accommodate enough concurrent users, connections that exceed the allocated number will be turned away.

### Running PopTop

Once you have configured the PPP layer and the PPTP daemon, make sure that the process starts with every system start:

```text
/usr/sbin/pptpd
```

Note that the `pptpd` daemon automatically sends itself to the background if invoked from a terminal. Don’t forget to set the Linux server to forward packets:

```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

PPTP uses destination port TCP 1723 on the Linux server and IP protocol ID 47 to exchange the data once the control connection has been established. If you are using Iptables to filter packets at the network layer, you need to allow these two ports through the filter.

Figure 12.10 illustrates a typical use of the PPTP protocol. One of ACME’s remote users is in a hotel room, dialing into the local ISP. That user has established a PPP session to the hub’s RAS that connects to ACME’s Boston PPTP server via IP end to end. If authentication is successful, the remote user sees a virtual interface on the laptop with the address 10.20.20.100. This interface “appears” to the Boston LAN as if it were a local interface. This allows the remote user to access resources in the local network 10.20.20.0/24 as if the laptop is physically connected to it.

![Figure 12.10](img/3258bbaf790525f8c4eb25fabff7844a_382_0.png)

## Configuring the PPTP Client on Windows 2000

Here is how to configure your users’ Windows 2000 Professional systems to connect to the Linux PPTP server that you’ve just built.
