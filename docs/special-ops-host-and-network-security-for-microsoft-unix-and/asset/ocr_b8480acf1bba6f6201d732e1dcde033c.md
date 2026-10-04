# Securing Exchange and Outlook Web Access • Chapter 7

Q: Do you think remote users can safely be allowed to read their e-mail on the internal network?

A: Yes. With reasonable precautions, I think remote users can be allowed into the network. For Outlook MAPI clients, I think the remote client should come in through a VPN connection.VPN connections can be made even secure with authentication devices such as SecureID. For other remote clients, I recommend using only OWA. Configuring an OWA front-end server in a well-secured DMZ provides a reasonable level of security.

Q: What three points should we focus on to get started that will give us the highest return for our investment?

A: For starters: a properly configured firewall, W2K/IIS/IE/E2K service packs, and Exchange-aware anti-virus software.

Q: How can administrators disallow the Exchange server to return internal IP addresses in the e-mail headers?

A: Exchange 2000 cannot strip out headers without custom programming. I recommend you use a third-party product such as the Cisco Firewall or Clearswift’s Mail Sweeper. Direct all outbound mail through one of these products and have it rewrite the SMTP headers so that internal hosts are removed from the SMTP header.

Q: Where are the biggest risks?

A: Most of the vulnerabilities associated with Exchange have actually come through IIS. That is why W2K/IIS/E2K service packs, IIS lockdown, and URLScan are so important.

Q: What do you see as the most neglected Exchange 2000 security procedures?

A: All of them! Servers that are directly exposed to the Internet; no service packs; missing or out-of-date virus scanning; non-existent tape media security procedures; no physical security; administrators that have access to all mailboxes.

![](bbox=[0.707, 0.943, 0.929, 0.971])