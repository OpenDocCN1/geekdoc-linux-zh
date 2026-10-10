
password. Thus, by adding a line to the pap-secrets file which specifies the empty string for the client and password, it is possible to allow restricted access to hosts which refuse to authenticate themselves.

## ROUTING

When IPCP negotiation is completed successfully, pppd will inform the kernel of the local and remote IP addresses for the ppp interface. This is sufficient to create a host route to the remote end of the link, which will enable the peers to exchange IP packets. Communication with other machines generally requires further modification to routing tables and/or ARP (Address Resolution Protocol) tables. In most cases the *defaultroute* and/or *proxyarp* options are sufficient for this, but in some cases further intervention is required. The /etc/ppp/ip-up script can be used for this.

Sometimes it is desirable to add a default route through the remote host, as in the case of a machine whose only connection to the Internet is through the ppp interface. The *defaultroute* option causes pppd to create such a default route when IPCP comes up, and delete it when the link is terminated.

In some cases it is desirable to use proxy ARP, for example on a server machine connected to a LAN, in order to allow other hosts to communicate with the remote host. The *proxyarp* option causes pppd to look for a network interface on the same subnet as the remote host (an interface supporting broadcast and ARP, which is up and not a point-to-point or loopback interface). If found, pppd creates a permanent, published ARP entry with the IP address of the remote host and the hardware address of the network interface found.

When the *demand* option is used, the interface IP addresses have already been set at the point when IPCP comes up. If pppd has not been able to negotiate the same addresses that it used to configure the interface (for example when the peer is an ISP that uses dynamic IP address assignment), pppd has to change the interface IP addresses to the negotiated addresses. This may disrupt existing connections, and the use of demand dialling with peers that do dynamic IP address assignment is not recommended.

## EXAMPLES

The following examples assume that the /etc/ppp/options file contains the *auth* option (as in the default /etc/ppp/options file in the ppp distribution).

Probably the most common use of pppd is to dial out to an ISP. This can be done with a command such as

```
pppd call isp
```

where the /etc/ppp/peers/isp file is set up by the system administrator to contain something like this

```
ttySO 19200 crtscts
connect `/usr/sbin/chat/chat -v -f /etc/ppp/chat-isp' 
noauth
```

In this example, we are using chat to dial the ISP's modem and go through any logon sequence required. The /etc/ppp/chat-isp file contains the script used by chat; it could, for example, contain something like this

```
ABORT "NO CARRIER"
ABORT "NO DIALTONE"
ABORT "ERROR"
ABORT "NO ANSWER"
ABORT "BUSY"
ABORT "Username/Password Incorrect"
"at"
OK "at&d0c1"
OK "atd2468135"
"name: " "^Umyserid"
"word: " "^U"
"ispts" "^Upq"
"^_" "^Up" "^_"
```

See the chat(8) man page for details of chat scripts.

Pppd can also be used to provide a dial-in ppp service for users. If the users already have login accounts, the simplest way to set up the ppp service is to let the users log in to their accounts and run pppd (installed setuidroot) with a command such as

```
pppd proxyarp
```

To allow a user to use the PPP facilities, you need to allocate an IP address for that user's machine and create an entry in /etc/ppp/pap-secrets or /etc/ppp/chap-secrets (depending on which authentication method the PPP implementation on the user's machine supports), so that the user's machine can authenticate itself. For example, if Joe has a machine called "joespce" which is to be allowed to dial in to the machine called "server" and use the IP address joespce.my.net, you would add an entry like this to /etc/ppp/pap-secrets or /etc/ppp/chap-secrets:

```
joespce server "Joe's secret" joespce.my.net
```

Alternatively, you can create a username called (for example) "ppp," whose login shell is pppd and whose home directory is /etc/ppp. Options to be used when pppd is run this way can be put in /etc/ppp/ppprs.

If your serial connection is any more complicated than a piece of wire, you may need to arrange for some control characters to be escaped. In particular, it is often useful to escape XON (^Q) and XOFF (^S), using asynmap 00000. If the path includes a telnet, you probably should escape '^' as well (asynmap 200a0000). If the path includes an rlogin, you will need to use the escape ff option on the end which is running the rlogin client, since many rlogin implementations are not transparent; they will remove the sequence [0xff, 0xff, 0x73, 0x73, followed by any 8 bytes] from the stream.

## DIAGNOSTICS

Messages are sent to the syslog daemon using facility LOG_DAEMON. (This can be overridden by recompiling pppd with the macro LOG_PPP defined as the desired facility.) In order to see the error and debug messages, you will need to edit your /etc/syslog.conf file to direct the messages to the desired output device or file.

The debug option causes the contents of all control packets sent or received to be logged, that is, all LCP, PAP, CHAP or IPCP packets. This can be useful if the PPP negotiation does not succeed or if authentication fails. If debugging is enabled at compile time, the debug option also causes other debugging messages to be logged.

Debugging can also be enabled or disabled by sending a SIGUSR1 signal to the pppd process. This signal acts as a toggle.

## FILES

- /var/run/ppprn.pid (BSD or Linux), /etc/ppp/pppn.pid (others) Process-ID for pppd process on ppp interface unit n.

- /etc/ppp/auth-up A program or script which is executed after the remote system successfully authenticates itself. It is executed with the parameters

```
interface-name peer-name user-name tty-device speed
```

and with its standard input, output and error redirected to /dev/null. This program or script is executed with the real and effective user-IDs set to root, and with an empty environment. (Note that this script is not executed if the peer doesn't authenticate itself, for example when the noauth option is used.)

- **/etc/ppp/auth-down** A program or script which is executed when the link goes down, if /etc/ppp/auth-up was previously executed. It is executed in the same manner with the same parameters as /etc/ppp/auth-up.

- **/etc/ppp/ip-up** A program or script which is executed when the link is available for sending and receiving IP packets (that is, IPCP has come up). It is executed with the parameters interface-name tty-device speed local-IP-address remote-IP-address ipparam and with its standard input, output and error streams redirected to /dev/null. This program or script is executed with the real and effective user-IDs set to root. This is so that it can be used to manipulate routes, run privileged daemons (e.g. sendmail), etc. Be careful that the contents of the /etc/ppp/ip-up and /etc/ppp/ip-down scripts do not comprise your system's security. This program or script is executed with an empty environment, so you must either specify a PATH or use full pathnames.

- **/etc/ppp/ip-down** A program or script which is executed when the link is no longer available for sending and receiving IP packets. This script can be used for undoing the effects of the /etc/ppp/ip-up script. It is invoked in the same manner and with the same parameters as the ip-up script, and the same security considerations apply.

- **/etc/ppp/ipx-up** A program or script which is executed when the link is available for sending and receiving IPX packets (that is, IPXCP has come up). It is executed with the parameters interface-name tty-device speed network-number local-IPX-node-address remote-IPX-node-address local-IPX-routing-protocol remote-IPX-routing-protocol local-IPX-router-name remote-IPX-router-name ipparam pppd-pid and with its standard input, output and error streams redirected to /dev/null.
