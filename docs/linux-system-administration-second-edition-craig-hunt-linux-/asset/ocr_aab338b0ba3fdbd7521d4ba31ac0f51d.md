thus reducing the spammer's own online time.

**Obscuring the origin** Using a mail relay obscures the origin of the spam. Each server through which a message passes adds a header that identifies the server and the system from which the server received the message. If a spammer uses a relay, the ultimate recipient may believe that the relay sent the message, thus deflecting blame. This strategy can be particularly effective if the spammer adds fake headers that indicate a bogus point of origin.

**Avoiding detection by the ISP** The spammer's own ISP may have the means to detect spam as it moves through its own system. Using another computer as a relay, thus bypassing the ISP's legitimate relay, can help the spammer avoid detection—probably not for long, but for long enough to make the minimal effort worthwhile.

It's safest to configure a Linux system to not relay mail at all. Sendmail can be configured to work in precisely this way, as it is by default in Red Hat 7.3. "Configuring Sendmail to Relay for a Domain," earlier in this chapter, described several means of allowing sendmail to relay legitimate e-mail. Some of these methods are extremely dangerous and should not be used. `promiscuous_relay` is the worst of these, followed by `relay_local` from and `relay_based_on_MX`. The best way to configure sendmail as a safe relay is to specify IP addresses in the `/etc/mail/access` file, as described in "Configuring Sendmail to Relay for a Domain." If this is impractical for some reason, `relay_entire_domain` is probably not too unsafe.

If you make any extensive changes to your sendmail configuration, it's best to test your system to be sure it's not an open relay. To do this, initiate a Telnet connection to mail-abuse.org *from the system you want to test*:

```
$ telnet mail-abuse.org
```

You should see in response the output of the MAPS system's attempts to use your system as a relay. The response should be a series of "relaying denied" messages, followed by a statement that the system blocked all relay attempts. If not, review your configuration to be sure you've not included any unwanted relaying options. You may also want to check for an updated version of sendmail from your distribution's provider, particularly if you're using an old version of sendmail—prior to version 8.9.0, sendmail's default configuration was to relay all mail.

# Stopping Incoming Spam

Blocking relays and outgoing spam is part of what it takes to be a good Internet citizen. Taking these steps will not, however, stop your users from being flooded with spam. To alleviate this problem, you must take additional steps. Two broad classes of spam filters are available: *blackhole lists*, which block spam based on a list of IP addresses you may want to refuse for one reason or another, and filters based upon header contents, such as message subject lines, or even message bodies.

**Warning** No system of spam detection is perfect; all spam filters produce occasional errors. These errors fall into two categories: *false alarms*, in which nonspam messages are mistakenly blocked, and *misses*, in which spam gets past the filter. Reducing the number of misses usually raises the number of false alarms and vice versa. You must decide how many legitimate e-mails you want to sacrifice when blocking spam and set your spam filters appropriately.

366