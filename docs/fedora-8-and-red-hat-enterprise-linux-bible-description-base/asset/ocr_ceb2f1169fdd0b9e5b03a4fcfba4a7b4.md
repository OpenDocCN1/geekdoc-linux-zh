```
```
To:spidermaker.com                RELAY
To:former-user@linuxtoys.net      ERROR: User no longer works here
```
```

On the `Connect:192.168` line, the network address (presumably the first part of the IP addresses used on your LAN) is allowed to relay mail. This is a good way to allow everyone sending mail from a machine on the local LAN to have their mail relayed. On the next line (`Connect:linuxtoys.net`), mail coming from any machine in the named domain is allowed to be relayed. The third line represents a domain that you know to be a spam relay, so you reject messages originating from that domain.

The next three lines indicate how to treat mail received for relaying, based on the From and To names associated with the message. As you can see, the first example allows relay of any messages from `chris@linuxtoys.net`. In the last example, mail being forwarded to a particular person (`former-user@linuxtoys.net`) is rejected and a custom error message (in this case *User no longer works here*) is sent back to the sender.

> NOTE: Use some caution when you are creating relay rules based on user e-mail address. Because those values are reported by the users themselves, they are vulnerable to being spoofed.

Once you have adjusted this file to suit you, you must rebuild the access database (`access.db` file) for the changes to take effect. See “Starting sendmail and generating database files” for information on this topic.

# ## Configuring virtual servers

If you have set up a sendmail mail server for one domain, it’s quite possible that you will someday want to have multiple domains served from that same computer. To create virtual servers on the same computer, you must add the name of every domain being served to the `/etc/mail/local-host-names` file.

For example, if your sendmail server were handling e-mail accounts for `linuxtoys.net`, `example.com`, and `example.net` domains, the `local-host-names` file would appear as follows:

```
```
# local-host-names - include all aliases for your machine here.
linuxtoys.net
example.com
example.net
```
```

Even if you are serving only one domain with your mail server, it is a good idea to identify that domain in this file. When messages come to the server for the domains listed here, sendmail knows to try to deliver the messages locally. Sendmail interprets messages for domains not listed here as needing to be relayed.