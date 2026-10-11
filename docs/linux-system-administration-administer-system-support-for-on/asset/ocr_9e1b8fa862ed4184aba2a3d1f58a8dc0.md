![](bbox=[0.05, 0.1, 0.16, 0.17])

Listserv is not freeware. If you are interested in the Listserv software, however, check out http://www.lsoft.com.

# Daemons

E-mail is managed by daemons such as POP3 (which enables you to download your mail remotely and read it off-line); IMAP (which enables you to read your mail remotely); and sendmail (which enables you to be the mail authority for a certain domain). Except for sendmail, these daemons, are managed by inetd, the net-working super-daemon. All work in a client-server model; the daemons perform as servers. POP3 and IMAP both let the users start the clients (Pine uses IMAP, and POP can be used with other clients such as xnih). To use a client with POP or IMAP, you don’t have to have the daemons running.

As with POP and IMAP, sendmail is a delivery agent – but its workings are a little more complicated. You can use sendmail to filter messages (for example), and you may find its design less friendly than that of POP or IMAP.

![](bbox=[0.06, 0.51, 0.16, 0.58])

Sendmail is known to be a major security hole. Additionally, some cleartext-related holes have appeared recently in IMAP and in POP (especially since they send passwords over the wire). If you’re going to use a mailer, first try using qmail instead. It’s not only easier to use, but more secure. You can find it at http://www.qmail.org.

# Using Client Applications

Several clients are available for the World Wide Web, including Netscape, as shown in Figure 12-4. Some Web browsers include the functionality needed to read e-mail or USENET news.