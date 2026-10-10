# Secure Remote Access

Remote access solutions in various organizations need to meet strict requirements in order to satisfy the needs of their end-users, which can range from road warriors working from hotel rooms to technical administrators working from home. While remote access solutions need to be available, functional, and flexible, security concerns often get overlooked. For example, how many remote users in your network use the following items to get access to company resources?

+   • SMTP and POP/IMAP to retrieve e-mail
+   • Dialup modems when inside Network Address Translated (NAT’d) Local Area Networks
+   • SMB or NFS for remote file access
+   • PPTP, VNC, or pcAnywhere for remote management

If your organization does have several people who do access internal resources with any of these items, especially with the second option, you probably could use SSH as a partial or full remote access solution. I cannot discuss the topic of remote access solutions without bringing up IPSec as the standard remote access solution. While IPSec might be the favorable solution for many remote access architectures, it might have limitations that may not make it the best solution for you. For example, its cost requirements, its setbacks in NAT’d