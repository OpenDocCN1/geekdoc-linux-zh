For Sendmail to work at all, it requires only that the OSTYPE and MAILERS macros be defined, along with any needed features and options. A very simple Sendmail file is shown here.

```
mysendmail.mc
dnl My sendmail.mc file
OSTYPE(`linux')
define(`PROCMail_MAILER_PATH', `/usr/bin/procmail')
FEATURE(`redirect')
MAILER(procmail)
MAILER(smtp)
```

A sendmail.mc file usually contains many more entries, particularly for parameters and features. Check the /etc/mail/sendmail.mc file on your Red Hat system to see the standard default entries for Sendmail.

# Sendmail Masquerading

For a mail server that is relaying messages from local hosts to the Internet, you may want to masquerade the source of the messages. In large networks that have their own mail servers connected to the Internet, Sendmail masquerading can make messages sent by local hosts appear to be sent by the mail server. Their host address will be replaced by the mail server's address. Returned mail can then be sent to the mail server and held in POP or IMAP server mailboxes that can be later accessed by users on the local hosts. Also, entries in the server's virtual user table could forward mail to corresponding users in local hosts.

Masquerading is often used to mask local hosts with a domain name. Any subdomains can also be masqueraded. This method can be applied to situations where an ISP or your network administrator has assigned your network its own domain name. You can then mask all mail messages as coming from your domain name instead of from particular hosts or from any subdomains you may have. For example, if a network's official domain name is mytrek.com, all messages from the hosts in the mytrek.com network, such as rabbit.mytrek.com and turtle.mytrek.com, could be masqueraded to appear as just coming from mytrek.com. Should the mytrek.com network have a subnetwork whose domain is mybeach.com, any messages from mybeach.com could also be masqueraded as coming from mytrek.com.

Masquerading is turned on with the MASQUERADE_AS command. This takes as its argument the name you want to masquerade your mail as. Normally, the name used is just the domain name, without the mail host. In the following example, the mail is masqueraded as simply mytrek.com. Mail sent from a local host like turtle.mytrek.com will appear to be sent by just mytrek.com:

```
MASQUERADE_AS(`mytrek.com')dnl
```

You will also have to specify the hosts and domains on your local network that your Sendmail server should masquerade. If you have decided to masquerade all the hosts in your local network, you just need to set the masquerade_entire_domain feature, as in:

```
FEATURE(`masquerade_entire_domain')dnl
```

If, instead, you want to masquerade particular hosts or your domain has several subdomains that you want masqueraded, you list them in the MASQUERADE_DOMAIN entry.