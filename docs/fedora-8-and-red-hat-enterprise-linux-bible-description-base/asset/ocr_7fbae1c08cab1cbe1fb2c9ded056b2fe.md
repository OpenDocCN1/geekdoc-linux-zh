Thunderbird for accessing newsgroups is that Thunderbird combines and decodes split yenc posts.

> **NOTE**: You can get the pan package by typing **yum install pan**.

Although Pan was originally designed for the GNOME desktop, GNOME libraries are no longer required to run Pan. For that reason, Pan will now work on KDE, Window Maker, or other desktop environments without any special software.

To open the Pan newsreader, type **pan** from the shell. The first time you start Pan, the Pan wizard runs to let you set up the newsreader. Have your e-mail address and your news server’s name ready. When the wizard is done, you can download the list of newsgroups available from your news server.

# Instant Messaging with Pidgin

Pidgin is the predominant instant messaging client in Linux. Originally based on the America Online (AOL) Open IM architecture (`www.aim.com`), the project recently changed its name to Pidgin from GAIM. Pidgin now supports a wide variety of instant messaging protocols, including the following:

+   * **Oscar** — Because Oscar is the official AIM protocol created by AOL, it is the most popular one used for Pidgin. To work in Pidgin, Oscar had to be reverse engineered because it is a proprietary protocol of AOL. So, not all features that you might find in AOL’s own instant messenger are supported. Messaging is done over TCP-based networks (typically, the Internet), with all messages going through AOL servers, except in the case of direct connections (which are difficult to get working properly).
+   * **MSN Messenger** — This protocol was based originally on the MSN Messenger Service 1.0 protocol (`www.hypothetic.org/docs/msn/ietf_draft.txt`). That protocol has been “enhanced” so significantly by Microsoft since it was first published that the version included with Pidgin had to be reverse engineered. To find out more about MSN Messenger (from Pidgin or otherwise), see the MSN Messenger Protocol Resources/Links page (`www.hypothetic.org/docs/msn/resources/links.php`).
+   * **ICQ** — Pidgin uses the open source icqlib library to implement the ICQ protocol. Because of recent changes to the ICQ protocol, it is usually recommended to use Oscar to connect to the ICQ network, rather than icqlib.
+   * **IRC** — The Internet Relay Chat protocol is based on the Internet standard RFC 1459. Although there are differences in implementation of that standard on different IRC servers, this TCP-based protocol should work fine on most IRC servers.
+   * **Yahoo! Messenger** — This allows you to communicate to others using Yahoo! Messenger servers.