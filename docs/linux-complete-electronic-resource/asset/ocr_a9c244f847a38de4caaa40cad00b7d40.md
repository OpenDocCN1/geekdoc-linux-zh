+   2. The firewall is set up to masquerade any packets coming from the private network and going to port 80 on an Internet host.

+   3. Netscape is configured to connect directly.

+   4. DNS must be configured correctly on the private network.

+   5. The firewall should be the default route (aka gateway) for the private network.

Netscape on myhost reads `http://slashdot.org`.

+   1. Netscape looks up the name `slashdot.org`, and gets 207.218.152.131. It then opens a connection to that IP address, using local port 1050 and asks the Web server (port 80) for the Web page.

+   2. As the packets from myhost (port 1050) to `slashdot.org` (port 80) pass through the firewall, they are rewritten to come from the PPP interface of the firewall, port 65000. The firewall has a valid Internet address (1.2.3.4) so reply packets from `www.linuxhq.com` get routed back OK.

+   3. As packets from `slashdot.org` (port 80) to `firewall.littlecorp.com` (port 65000) come in, they are rewritten to go to myhost, port 1050. This is the real magic of masquerading: it remembers when it rewrites outgoing packets so it can write them back as replies come in.

+   4. Netscape renders the page.

From `slashdot.org`'s point of view, the connection is made from 1.2.3.4 (firewall's PPP interface) port 65000 to 207.218.152.131 (`slashdot.org`) port 80. From myhost's point of view, the connection is made from 192.168.1.100 (myhost) port 1050, to 207.218.152.131 (`slashdot.org`) port 80.

# Public Network

In this scenario, your personal network is a part of the Internet: Packets can flow without change across both networks. The IP addresses of the internal network must be assigned by applying for a block of IP addresses, so the rest of the network will know how to get packets to you. This implies a permanent connection.