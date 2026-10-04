# Chapter 16 · Network Architecture

As you can see in Figure 16.10, the trace shows that my computer sent SNMP requests to the router, IP address 10.20.5.2, via port 161. On the right-hand side, you can see in clear the community string used “public” in clear text for the taking. The next step (Figure 16.11) will demonstrate the use of IP Network Browser in SolarWinds to enumerate the route.

You can easily see how damaging this information can be. Immediately, I have access to information regarding the router interfaces, IOS, ARP tables, and routes. Next, I can click the Config button on the toolbar to see this Community String to download the running Cisco configuration (Figure 16.12).

# Figure 16.12 IP Network Browser Router Enumeration

![](bbox=[0.233, 0.321, 0.766, 0.574])

Figure 16.12 shows the first page of your router's configuration file. You can see the encrypted enable password in file, as well as the IOS version (12.0), and at the bottom you can see the next step to click on the Decode button in the toolbar. This will launch SolarWinds Cisco password decoder. It is important to note that the decoder will be able to decode only the Telnet or console passwords. The enable secret password, denoted by the long string, use a different encryption algorithm, as opposed to the enable password or console/Telnet password, which use weak encryption (see Figure 16.13).

In the window shown in Figure 16.13, you can see the XOR'd password prior to decoding. Next, I can click the Decode button on the toolbar to see the encrypted passwords (see Figure 16.14).

Voila, the passwords appear to us in clear text. Now, we have two methods to gain access to these boxes; first, we can Telnet to them and use the Line Vry 0 4