# # Summary

+   - a firewall is a secure single point of entry and exit for your network. It controls all traffic passing through it on the basis of rules you specify
+   - if you're connected to the Internet, you need a firewall
+   - there are several types of firewall – packet-filtering, stateful packet inspection, application-gateway (or proxy), and hybrid. Each has advantages in terms of performance, level of security, and ease of configuration
+   - a demilitarized zone is a half-way-house network between the external Internet and your internal LAN:
+     - the DMZ is used for servers that are accessible from the Internet
+     - the firewall controls traffic from the Internet to the DMZ and from the DMZ to your LAN, giving you an extra layer of protection should any DMZ server be compromised
+     - servers on the DMZ (e.g. Web, HTTP, or DNS) usually fulfill a different role to servers running the same protocols on the internal LAN
+   - troubleshooting with a firewall in place is made harder because the firewall interferes with the traffic. Using two sniffers, one on the LAN inside the firewall and the second outside, often gives you the information you need to diagnose what's happening.

# ## What's next?

The next chapter covers other security systems for your Internet gateway – the point of connection of your network to the Internet: filtering Web traffic on the basis of the URLs specified and on the content of pages, blocking spam e-mail, and virus-scanning. Depending on your systems, many of these may tie in with your firewall.

In Chapter 27 we cover VPN, which can improve the security of connections to your site from branch offices and from dial-up users.

# ## Notes and further reading

Don't forget to include your firewall in the contingency plans you drew up in Module 23.10. We explain “personal firewalls,” for single dial-up machines, in Chapter 27's Notes. In Module 24.6 we mentioned Win-2K's Security Templates. For more information see:

+   ☐ http://www.microsoft.com/windows2000/en/server/help/sag\_SCWhatis.htm
+   *Security Templates Overview*

A few RFCs give general security guidelines. These are now dated, but the general approach is still valid:

+   ☐ RFC-2916 September 1997 *Site security handbook*
+   
+   ☐ RFC-2504 February 1999 *Users' Security Handbook*
+   
+   ☐ RFC-2828 May 2000 *Internet Security Glossary*