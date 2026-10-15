
## Tip

You can either set the default policy to ACCEPT and then explicitly deny unwanted connections, or set the default policy to DENY and explicitly accept connections you desire. The latter is generally more secure, but trickier to configure because you must understand the implications of each service you need. You can set the defaults independently for the input, output, and forward chains. For instance, you might set the default for input to DENY and the default for output to ACCEPT.

- Spoofing protection—The script blocks traffic that’s destined for the internal network originating from the external network, but that claims to come from the internal network, and vice-versa. When a packet claims to come from the network to which it’s going, that’s a sure sign that the address has been spoofed, or changed in what is likely a break-in attempt.
- Outgoing blocks—The script blocks outgoing traffic to two IP networks on port 80 (used for Web browsing). These addresses are used by ad.doubleclick.net, which provides ads for Web pages. Blocking such traffic can speed up Web browsing of some ad-laden pages. (On the other hand, in some cases such a block can also cause a Web page access to hang while the browser waits for images that will never come.) You could use similar blocks to prevent access to X-rated Web sites, software piracy sites, and so on. One drawback of using such blocking for X-rated or piracy sites is that the number of such sites is quite large and is constantly changing, which makes for a great deal of administrative effort.

## Note

Blocking the output chain request for a connection results in no return data, hence reducing network bandwidth. You could block return data (on the input chain) instead of or in addition to the output request, but using input blocking exclusively won’t result in a reduction in traffic to or from your firewall.

- Service controls—The script blocks telnet service from the external network. It also blocks attempts to access an X font server from the external network, while explicitly allowing such access from the host computer itself.

In most real packet filter scripts, you should include many more service controls than I present in this sample script. Such configurations can become quite complex. If you need fine control over your firewall, you should plan on investing a significant amount of time in setting up and testing your configuration.

In addition to DENY, you can configure your system to REJECT packets. The difference is that DENY makes the packets vanish without a trace, whereas REJECT sends a notice back to the originating machine that the packet was rejected. The latter is the usual behavior when a service isn’t running on a Linux computer.

## TIP

You can test whether you’ve successfully blocked a service or port using a Linux or UNIX telnet program. For instance, suppose you’re trying to block access to the local SSH server from external sites, but not from internal ones. Log onto an external computer and use telnet to attempt to access the firewall’s port 22, which is used for SSH access, as in

```
telnet gingko.biola.com 22
```

If you get a connection refused error message or no reply, you’ve successfully rejected or denied access, respectively. If you get a connected message, with or without further prompts, you’ve connected to the port and need to reexamine your configuration.

In testing your firewall, you may want to set up a test machine as a firewall between your regular network and a small test network of one or two computers. You can then test your firewall and its rules without disrupting the functioning of your main network. When you’re satisfied with the results, install your firewall script on the main firewall computer (making any necessary changes to the IP addresses first). You should do this when the main network isn’t being used heavily, though, in case there are problems.

## Setting Up a Proxy Server

There are several different proxy servers available for Linux. This section provides an overview of using one of them, SOCKS5 (Sockets version 5). Another popular proxy server available for Linux is the Firewall Toolkit (FWTK) from Trusted Information Systems (TIS). You can find out more about TIS and FWTK from http://www.tis.com.

## Installing and Configuring SOCKS

You can obtain the SOCKS software from the Web site http://www.socks.nec.com/. The software is available only in source code form, so you need to compile and install it.

## Compiling SOCKS
