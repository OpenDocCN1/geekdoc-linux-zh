# Introduction to Linux

The home page is at SourceForge \textless http://sourceforge.net/projects/xchat/\textgreater.

+   - aMSN: an MSN clone.
+   
+   - Konversation, kopete, KVIrc and many other K-tools from the KDE suite.
+   
+   - gnomeeeting: videoconferencing program for UNIX (now Ekiga).
+   
+   - jabber: Open Source Instant Messaging platform, compatible with ICQ, AIM, Yahoo, MSN, IRC, SMTP and much more.
+   
+   - psi: jabber client, see the PSI Jabber Client Homepage \textless http://psi.affinx.com/\textgreater.
+   
+   - skype: program for making telephone-like calls over the Internet to other Skype users, see \textless http://www.skype.com\textgreater for more info. Skype is free but not open.
+   
+   - Gizmo: a free (but not open) phone for your computer, see \textless http://www.gizmoproject.com\textgreater.

# **10.3.6** News services

Running a Usenet server involves a lot of expertise and fine-tuning, so refer to the INN homepage \textless http://www.isc.org/\textgreater for more information.

There are a couple of interesting newsgroups in the comp.* hierarchy, which can be accessed using a variety of text and graphical clients. A lot of mail clients support newsgroup browsing as well, check your program or see your local Open Source software mirror for text clients such as tin, slrn and mutt, or download Mozilla or one of a number of other graphical clients.

Deja.com \textless http://deja.com/\textgreater keeps a searchable archive of all newsgroups, powered by Google. This is a very powerful instrument for getting help: chances are very high that somebody has encountered your problem, found a solution and posted it in one of the newsgroups.

# **10.3.7** The Domain Name System

All these applications need DNS services to match IP addresses to host names and vice versa. A DNS server does not know all the IP addresses in the world, but networks with other DNS servers which it can query to find an unknown address. Most UNIX systems can run named, which is part of the BIND (Berkeley Internet Name Domain) package distributed by the Internet Software Consortium. It can run as a stand-alone caching nameserver, which is often done on Linux systems in order to speed up network access.