2.  As the packets from myhost (port 1050) to `slashdot.org` (port 80) pass through the firewall, they are redirected to the waiting transparent proxy on port 8080. The transparent proxy opens a connection (using local port 1025) to 207.218.152.131 port 80 (which is where the original packets were going).

3.  As the proxy receives the Web page from its connection to the Web server, it copies the data to the connection from Netscape.

4.  Netscape renders the page.

From `slashdot.org`'s point of view, the connection is made from 1.2.3.4 (firewall's PPP interface) port 1025 to 207.218.152.131 (`slashdot.org`) port 80. From myhost's point of view, the connection is made from 192.168.1.100 (myhost) port 1050, to 207.218.152.131 (`slashdot.org`) port 80, but it's actually talking to the transparent proxy.

# Private Network: Masquerading

In this scenario, packets from the private network never traverse the Internet without special treatment, and vice versa. The IP addresses of the private network should be assigned from the RFC1597 Private Network Allocations (that is, 10.*.*.*, 172.16.*.* or 192.168*.*).

Instead of using a proxy, we use a special kernel facility called *masquerading*. Masquerading rewrites packets as they pass through the firewall, so that they always seem to come from the firewall itself. It then rewrites the responses so they look like they are going to the original recipient.

Masquerading has separate modules to handle "tricky" protocols, such as FTP, RealAudio, Quake, etc. For really hard-to-handle protocols, the auto forwarding facility can handle some of them by automatically setting up port forwarding for related sets of ports: look for `ipportfw` (2.0 kernels) or `ipmasqadm` (2.1 kernels).

Any services you wish the Internet to access must be on the firewall. (But see the "Limited Internal Services" section later in this chapter.) Example: Allowing Web access from private network to the Internet.

+   1. The private network is assigned 192.168.1.* addresses, with myhost being 192.168.1.100, and the firewall's ethernet interface being assigned 192.168.1.1.