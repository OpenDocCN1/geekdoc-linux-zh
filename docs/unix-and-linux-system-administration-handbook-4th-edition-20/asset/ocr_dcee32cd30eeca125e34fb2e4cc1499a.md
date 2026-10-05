# Submission agents

moved beyond the text era, text-based user agents are no longer practical for most users. We shouldn't throw /bin/mail away; it's still a handy interface for scripts and other programs. (One avid Linux user we know routes nightly emails from cron to calendaring software that a glance at the calendar tells him status of all his software. By default, cron uses /bin/mail to notify a user when it cannot run a scheduled job.)

One of the elegant features illustrated in Exhibit A is that a user agent necessarily need to be running on the same system—or even on the same platform—as the rest of your mail system. Users can reach their email from any Windows laptop or smartphone through access protocols like IMAP and POP.

Wikipedia's "comparison of e-mail clients" contains a detailed list of many clients, the operating systems they run on, and the features they support. Popular clients include Thunderbird, Alpine, Zimbra, and of course, Microsoft Outlook. The "comparison of webmail providers" has similar information for web-based services like Gmail, Hot, and Yahoo!

# Submission agents

MSAs, a late addition to the email pantheon, were invented to offload the computational tasks of MTAs. MSAs make it easy for mail hubs to distinguish incoming from outbound mail (when making decisions about allowing laying, for example) and give user agents a uniform and simple configuration for outbound mail.

The MSA is a sort of "receptionist" for new messages injected into the system by local user agents. An MSA sits between the user agent and the transport agent and takes over several functions that were formerly part of the MTA's job. An MSA implements secure (encrypted and authenticated) communication with user agents and often do minor header rewriting and cleanup on incoming messages. In many cases, the MSA is really just the MTA listening on a different port with a different configuration application.

MSAs speak the same mail transfer protocol used by MTAs, so they appear to be MTAs from the perspective of user agents. However, they listen for connections on port 587 rather than port 25, the MSA standard. For this scheme to work, user agents must connect on port 587 instead of port 25. If your user agents cannot be taught to use port 587, you can still run an MSA on port 25, but you must do so on a system other than the one that runs your MSA; only one at a time on a particular port.

An MSA can help with several spam-induced problems. Infected home PCs are being used to send large amounts of spam. As a result, many ISPs offer home service either blocking connections to port 25 or require account verification as part of the SMTP conversation. A home PC could use the ISP's own mail server for outgoing mail, but some of the newer spam-fighting mechanisms much

![](bbox=[0.953, 0.225, 0.992, 0.355])