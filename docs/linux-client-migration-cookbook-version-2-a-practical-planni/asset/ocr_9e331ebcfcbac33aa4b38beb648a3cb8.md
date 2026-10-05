management policies that focus on a "compartmentalizing the breach" strategy. The basic idea in this strategy is to protect user space from non-user space processes. This strategy is supported by the fact that modern desktops are adding more and more "services" by default (that is, client applications that need network connectivity and awareness in relation to other client and server applications in the domain). It would be onerous to support application level compartmentalization for every desktop application needing it; instead, because of the fact that desktop systems do not need to meet stringent availability requirements, you focus on a strategy that affords high levels of security (compartmentalization) to just specific file systems on the client that are used to store the most sensitive data. "In order to achieve this goal, the community and independent software vendors (ISVs) must work with the SELinux developers to produce the necessary policies.\^2

+   Novell's AppArmor^3 provides a Linux network security framework. AppArmor was originally developed by Immux, Inc. Novell acquired Immux in 2005, and AppArmor is now included in the SUSE Linux Enterprise 10 products. AppArmor is an open source project.^4 The approach that AppArmor takes is different than SELinux, and they are currently seen as competing products. Novell maintains an extensive FAQ for AppArmor at:

```
http://developer.novell.com/wiki/index.php/Apparmor_FAQ
```

Because of its dominant share in the desktop computing market, coverage of Windows security concerns (the latest exploits, viruses, patches, and so) receives a lot of attention in the IT press relative to those same set of concerns on Linux. That does not mean that security concerns disappear when you migrate to Linux. But when you consider the open "UNIX-like" architecture of Linux and the fast response dynamics of open source community development, Linux presents a very compelling option when the goal is to lower the total cost involved in providing secure client platforms.

Even though Linux has many security-related features or properties, we concentrate on the relevant to a Linux client. Because a Linux client there is interactive user activity, the security issues we look at reflect. We focus on the features most related to this interactive user activity and others that are also relevant:

+   Browser search
Messaging-client security
User fencing and security
Bugfix response time
Modularity of the operating system
Firewalling

> ^2 From the Fedora Core 5 SELinux FAQ: http://fedora.redhat.com/docs/selinux-faq-fc5/
^3 http://www.novell.com/linux/security/apparmor/overview.html
^4 http://en.opensource.org/AppArmor

28 Linux Migration Handbook Cookbook, Version 2