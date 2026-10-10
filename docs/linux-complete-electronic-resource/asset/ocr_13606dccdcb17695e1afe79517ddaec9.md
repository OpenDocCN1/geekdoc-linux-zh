# IP Chains

The only way things ever connect to the Internet is by connecting to the firewall, which is the only machine on both networks that connects onward. You run a program (on the firewall) called a proxy to do this (there are proxies for FTP, Web access, telnet, RealAudio, Usenet News and other services). See the Firewall HOWTO.

Any services you wish the Internet to access must be on the firewall. (But see the “Limited Internal Services” section later in this chapter.)

Example: Allowing Web access from private networks to the Internet.

+   * The private network is assigned 192.168.1.\* addresses, with myhost being 192.168.1.100 and the firewall's ethernet interface being assigned 192.168.1.1.
+   * A Web proxy (for example, “squid”) is installed and configured on the firewall, running on, say, port 8080.
+   * Netscape on the private network is configured to use the firewall port 8080 as a proxy.
+   * DNS does not need to be configured on the private network.
+   * DNS does need to be configured on the firewall.
+   * No default route (aka gateway) needs to be configured on the private network.

Netscape on myhost reads `http://slashdot.org`.

+   1. Netscape connects to the firewall port 8080, using port 1050 on myhost. It asks for the Web page of `http://slashdot.org`.
+   2. The proxy looks up the name `slashdot.org`, and gets 207.218.152.131. It then opens a connection to that IP address (using port 1025 on the firewall's external interface) and asks the Web server (port 80) for the Web page.
+   3. As it receives the Web page from its connection to the Web server, it copies the data to the connection from Netscape.
+   4. Netscape renders the page.

From `slashdot.org`'s point of view, the connection is made from 1.2.3.4 (firewall's PPP interface) port 1025 to 207.218.152.131 (`slashdot.org`) port 80. From myhost's point of view, the connection is made from 192.168.1.100 (myhost) port 1050, to 192.168.1.1 (firewall's ethernet interface) port 8080.

![](bbox=[0.9, 0.55, 0.99, 0.63])