+   2. The MTA at lion.org receives user1's email message and queues it for delivery behind any other messages that are also waiting to go out.

+   3. The MTA at lion.org contacts the MTA at cheetah.org on port 25. After cheetah.org acknowledges the connection, the MTA at lion.org sends the mail message. After cheetah.org accepts and acknowledges receipt of the message, the connection is closed.

+   4. The MTA at cheetah.org places the mail message into user2's incoming mailbox; user2 is notified that she has new mail the next time she logs on.

Of course, several things can go wrong during this process. Here are a few examples:

> What if user2 doesn't exist at cheetah.org? In this case, the MTA at cheetah.org will reject the email and notify the MTA at lion.org of what the problem is. The MTA at lion.org will then generate an email message and send it to user1@lion.org, informing her that no user2 exists at cheetah.org (or perhaps just silently discard the message and give the sender no indication of the problem, depending on how the email server is configured).

> What happens if cheetah.org doesn't respond to lion.org's connection attempts? (Perhaps the server is down for maintenance.) The MTA at lion.org notifies the sender that the initial delivery attempt has failed. Further attempts will be made at intervals decided by the server administrator until the deadline is reached, and the sender will be notified that the mail is undeliverable.

# The Mail Transport Agent

Working behind the scenes to move mail between computers on different networks, several different MTAs are available for Fedora Core—each with its own strengths and weaknesses. Some are extremely powerful, but very difficult to configure and somewhat slow; others are very fast and easy to configure, but do not contain as many features. The following sections provide more details about some of the more common MTAs available for use with Fedora.

# Sendmail

The vast majority of email traffic on the Internet is handled by an MTA called Sendmail, the default MTA shipped with Fedora (and a number of other Unix distributions). Sendmail has the advantage of being installed and well-supported in your Fedora system. The commercial version (not included with Fedora) sports a GUI configuration utility, as well.

Sendmail is one of the oldest and most powerful MTAs in existence, but it has a few disadvantages. It is somewhat slow; in a high load environment, other MTAs, including Postfix and Qmail, typically can handle a much greater volume of messages per second. Sendmail is also notoriously convoluted; configuration files are extremely cryptic. (The best-selling book on Sendmail is more than 1,000 pages in length.)

Fortunately, the default configuration of Sendmail as provided by Fedora Core works fine for most basic installations, and only minor changes are needed to configure it for a basic