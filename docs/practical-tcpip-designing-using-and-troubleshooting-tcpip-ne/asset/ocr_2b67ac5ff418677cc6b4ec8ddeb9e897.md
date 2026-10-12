+   for manual keying, we start with very simple keys that we can easily read and check over the phone. We use “0123456789abcdef” for a 16-digit key and the same thing repeated twice for a 32-digit key. (But make sure you change them to something less easily guessed as soon as the link is working!)

+   ISPs often block the IPsec AH and ESP protocols by default. (It’s more unusual to have IKE blocked, because it runs over UDP) Before you even start installing your VPN, check that the ISPs at both ends allow protocols 50 and 51 (ESP, AH) and UDP port 500 (IKE) in and out of their networks

+   many ISP services for home users (e.g. cheap or free phone calls to the ISP, and some ADSL or cable modem services) deliberately block ESP and AH, since they are only used by business customers. You may have to pay extra to have these blocks removed

+   if you have your laptop set up to VPN to the office (e.g. to 10.*.*) and later bring it into the office and connect up to the LAN, traffic for 10.*.* will still be VPNed. (Typical symptoms are that ARPs succeed – arp –a shows other machines – but no other TCP/IP traffic is transmitted on the wire.) You need to either manually disable the VPN when on the LAN, or enable VPNing only on the dial-up interface (cf. Module 26.10.)

+   because IPsec is an evolving standard and IKE is very complex, not all implementations inter-operate with one another or support all options. This will become less of a problem in time, as implementations are tested and improved (and maybe IKE will be replaced with something better – see Notes). In the meantime, you may have to restrict yourself to option combinations that your VPN manufacturer recommends

+   if you’re using Microsoft Windows Networking over VPN, remember that your network now involves routers, so you’ll have to use WINS (or an LMHOSTS file) if you want NetBIOS name resolution and network browsing to operate correctly (c.f. Module 26.11).

In the next module we explain how to integrate a test network with your live LAN, to simplify troubleshooting and to check out your configurations before you actually deploy them live.

![](bbox=[0.18, 0.62, 0.75, 0.91])

Figure 27.14 Use tcpdump outside your firewall to see encrypted VPN packets