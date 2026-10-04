AVAPI 2.0 aware products are capable of scanning the e-mail after it arrives on the Exchange server, but before the user is notified the message is in their mailbox. Some API-only-based solutions may actually allow a message to arrive in the user's mailbox before the message gets scanned.

# SMTP Virus Scanners and Content Inspection

There is a wide variety of SMTP mail scanners on the market today. These scanners do not depend on any single e-mail vendor or platform (Windows or Unix), but perform the scanning and content inspection on messages prior to the message being delivered to the mail server. In most cases, the DNS MX records point to these SMTP scanners rather than to your Exchange server; the SMTP scanner inspects the message and forwards on to an Exchange server.

I have implemented a number of these systems with great success, but I recommend a different vendor for your SMTP scanner than you use for your Exchange server. For example, if you use Norton Anti-Virus for Exchange on your Exchange 2000 servers, Trend's VirusWall product as an SMTP scanner. This ensures that you have two different vendors inspecting your e-mail, which greatly improves the chances for catching viruses before they arrive at the user's desktop.

> NOTE
Many organizations implement anti-virus systems from different vendors not only at the SMTP scanner, but also for the client and Exchange server.

Many firewall products today will also perform virus and content inspection as SMTP traffic comes through the firewall. Depending on the size of your organization and how overwhelmed your firewall is, this may be a good place or a bad place to implement SMTP mail scanning. If the firewall is heavily burdened, scanning SMTP traffic will only make matters.

Some of these SMTP scanners are more simple than virus scanners, such as Clearsmith's Mail Sweeper (formerly MIMESweeper) or GFI's Mail Se, can scan through a message looking not only for viruses, but also things that indicate that the message is spam or that the message contains sensitive or objectionable material.

If you are implementing a content inspection system, you may want to use it not only to inspect inbound e-mail, but also direct outbound mail through this