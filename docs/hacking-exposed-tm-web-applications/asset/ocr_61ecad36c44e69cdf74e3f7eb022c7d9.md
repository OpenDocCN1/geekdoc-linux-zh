# Hacking Exposed Web Applications

ones!) and automatically determines if you already have the correct version. However, we don't think this convenient site is justification for leaving ActiveX enabled all the time. Even more frustrating, when ActiveXScript is disabled under IE, the autosearch mechanism that leads the browser from a typed-in address like “mp3” to http://www.mp3.com does not work.

One solution to this problem is to manually enable ActiveX when visiting a site and then manually shut it off again. The smarter thing to do is to use the Trusted Sites security zone. Assign lower level of security (we recommend) to use this zone, and add trusted sites like WU (windowsupdate.microsoft.com) to it. Way, when visiting WU, the weaker security settings apply and the site's ActiveX features still work. Similarly allow search from the address bar. Aren't security zones convenient?

When configuring security zones, be sure to select which zone you want to apply content displayed in the main reader. We strongly recommend setting it to Restricted Sites (This is the default setting in Outlook 2000 for the security update patch, and later versions). Make sure that the Restricted Sites are configured to disable all active content! This sets it to High, and then use the Custom button to go back and manually disable everything that High leaves open (Or set them to high safety if disabling is not available). Figure 12-3 shows how to configure Outlook for Restricted Sites. So, to summarize our recommendations for IE Security Zones:

+   Configure the Internet zone according to Table 12-1.
* Assign a setting of Medium to the Trusted Sites zone, and manually add sites to that zone you trust to run active content.
* Disable everything in the Restricted Sites zone.
Configure Outlook/Outlook Express to use the Restricted Sites to read e-mail.

Server-Side Countermeasures Based on the sample attacks we have demonstrated, server-side countermeasures for active content exploits should be fairly obvious: dont implement technology that can be subverted to attack your end-users or customers.

This advice is particularly relevant to ActiveX. If you are planning on implementing an ActiveX control to lend client-side functionality to your Web application, you should carefully consider the following guidelines:

+   Don't mark the control “safe” if at all; if you do mark it safe, ensure that it performs only the most benign functions and subject it to independent security review.
Write/distribute well-written controls, don't perform privileged actions (like launch files named setup.ex.).
Be prepared to rapidly patch vulnerabilities as they are found (for example, Gator Corp. released a patch to the Gator Setup control, now available on the Gator Web site; see “References and Further Reading”.