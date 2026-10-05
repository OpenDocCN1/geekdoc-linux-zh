# OffSec

As before, if we wanted to manually confirm that port 9999 is listening on CONFLUENCE1, we would exploit the Confluence vulnerability again to get another reverse shell (since our existing shell is tied up with the SSH port forward command), then we run ss in shell.

As we did earlier, let's connect to port 445 to HRSHRES. However, this time we will do it through the SOCKS proxy port created by our SSH dynamic port forward command.

To accomplish this, we'll use smclient agent. However, we find smclient doesn't natively provide an option to use a SOCKS proxy.918 Without a native option to use a SOCKS proxy in smclient, we can't take advantage of our dynamic port forward. The SOCKS proxy can't determine how to handle traffic in the SOCKS protocol format.

To use smclient in this situation, we'll leverage Proxchains.919 Proxchains is a tool that force network traffic through third party tools over HTTP or SOCKS proxies. As the name suggests, it can also be configured to push traffic over a chain of concurrent proxies.

> The way Proxchains works is a light hack. It uses the Linux shared object preloading technique (LD_PRELOAD) to hook libc networking functions within the binary that gets passed to, and forces all connections over the proxy server. This might not work for everything, but it will work for most dynamically-linked binaries that perform simple network operations. It won't work on statically-linked binaries.

Let's try Proxchains with smclient. Proxchains uses a configuration file for almost everything, stored by default at /etc/proxys4.conf. We need to edit this file to ensure Proxchains can locate our SOCKS proxy port, and confirm that it's a SOCKS proxy (rather than any other kind of proxy). By default, proxies are defined at the end of the file. We can simply replace any existing proxy definition in that file with a single line defining the proxy type, IP address, and port of the SOCKS proxy running on CONFLUENCE1(socks5 192.168.50.63 9999).

> Although we used socks5 in this example, it could be socks4, since SSH supports both.OCKS5 supports authentication, IPv6, and User Datagram Protocol (UDP), including DNS. Some SOCKS proxies will only support the SOCKS4 protocol. Make sure you check which version is supported by the SOCKS server when using SOCKS proxies in engagements.

After editing the file, it should appear as follows:

918 (Samba, 2022), https://www.samba.org/samba/docs/current/man-html/smclient.1.html
919 (r01, 2022), https://github.com/r01/proxchains-ng