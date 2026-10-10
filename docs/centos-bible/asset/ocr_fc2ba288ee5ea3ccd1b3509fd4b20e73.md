you quickly and use your machine to relay their spam. The results of a spammer using your machine can include the following.

+   - **You Can End Up on Blacklists** — Some e-mail blacklist maintainers look for open relays themselves and block them before abuse is even reported. Servers that use those blacklists will block all mail from you, even legitimate e-mail.
+   - **People Will Hate You** — Your mail server will be identified as the one sending the spam. As a result, people may retaliate against your server, or at the very least really wish you would stop sending them ads to help them get out of debt or enhance themselves in some way.
+   - **You Face Possible Fines and Jail** — More and more laws are being written to try to stop the spread of spam. You could be found guilty of negligence or have your machines shut down or confiscated, even if you didn't initiate the spam yourself.

This section describes how to set up the Sendmail access file (/etc/mail/access) to include a sensible set of rules defining for whom your server will relay mail. Using the access file, Sendmail can make decisions about whether or not to relay a message based on the sender's host/domain name, IP address, or e-mail address. You can further refine the match by checking for those addresses in Connect, From, or To data associated with the message.

There are then four basic actions you can have the server take on a match:

+   - **RELAY** — Your mail server could simply send the message on to the mail server requested in the mail message.
+   - **REJECT** — The message is rejected (not relayed), and the sender is told it was rejected.
+   - **DISCARD** — The message is silently discarded, and the sender is not told.
+   - **ERROR: text you choose** — You can add some informative text here, to give the sender some reason why the relay did not occur.

The /etc/mail/access file, by default, relays messages only from users who are directly logged into the mail server (localhost). Without being explicitly allowed, users from all other machines are not allowed to relay messages. Here's how the access file is set up by default:

```
```
Connect:localhost.localhost.localdomain      RELAY
Connect:localhost                             RELAY
Connect:127.0.0.1                             RELAY
```
```

With these defaults set, only mail sent from the local machine is relayed. So, if the only outgoing mail you send is sent while you are logged in directly to the server, you don't need to change this file. The following examples illustrate how you can selectively choose to relay or reject mail received by your Sendmail server:

```
```
Connect:192.168.*                             RELAY
Connect:example.com                             RELAY
Connect:spammer-domain.com                      REJECT
```
```