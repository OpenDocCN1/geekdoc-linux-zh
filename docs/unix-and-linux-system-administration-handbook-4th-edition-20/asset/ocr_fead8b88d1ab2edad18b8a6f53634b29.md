# Chapter 20 Electronic Mail

original SMTP connection is still open. Outgoing email can be scanned for viruses and spam on an internal smart host through which all messages are routed.

We suggest the following order of operations for sanity-checking a message:

+   - Checking RFC compliance of the sender's SMTP implementation
- Verifying the existence of local recipients
- IP blocking; see page 766
- Reputation checking; see page 766
- DKIM and SPF verification; see page 767
- Antispam filtering; see pages 764 and 765
- Antivirus scanning; see pages 768 and 769

Many spam robots do not follow the SMTP protocol correctly; they typically start before the EHLO response. A slight delay by your server can expose their "early talker" behavior. You can use this information to reject the connection or to increase the spam score of the received messages.

Checking recipients to verify that they are valid local users is good unless your later checks might transform recipients' addresses. Early checking minimizes the work your mail server has to do for mail that will eventually turn out to be undeliverable. It also eliminates lot of "shotgun" spam. However, it does let the sender probe your user address space.

The order of the other checks is primarily driven by their cost. Quick check and easy things before time-consuming things, that, on average, bad messages are refused as soon as possible.

Once you have identified a message as bad, what do you do with it? Refuse, drop, quarantine it, archive it? We recommend you quarantine and archive while you are testing your setup. When you are satisfied that the system is doing what you want, refuse or drop all viruses and refuse or archive spam, according to users' preferences. Delete archived spam that is more than a month old; while, users can move false positives from the spam box to their regular mailbox.

# Spam

Spam is the jargon for junk mail, also known as unsolicited commercial email or UCE. It becomes a serious problem because although the response per dollar is low (A list of 30 million email addresses costs $40). If it didn't work for spammers, it wouldn't be such a problem. Surveys show that 95%–98% of all mail is spam. Refer to spammological sites like spamhaus.net for the latest numbers.

Our main recommendation regarding spam is that you use the preventive measures and publicly maintained blacklists that are available to you. A good one is zen.spamhaus.org. Another possibility is to redirect your incoming mail to an outsourced spam fighting company such as Postini (now part of Google) or we