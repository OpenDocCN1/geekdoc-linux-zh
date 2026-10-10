you have an active mail server, you should be able to see emails coming in for other users. If you see other email activity, then the mail server is functioning in general and the next step is to pore through the logs. On the other hand, if you have a mostly inactive mail server or you aren’t seeing new log entries, the best next step is to perform the same steps as a remote mail server, only manually. Before you do that, though, if you truly aren’t getting any incoming email and you suspect you should, you may want to perform a quick `dig` query and confirm that your incoming mail server is listed as one of the mail servers for your domain and that its IP address is correct:

```
$ dig example.net MX
```

Now that you have confirmed that your mail server is listed in DNS, it’s time to simulate a remote mail server. To do this, get onto a machine, ideally one that’s outside of your network, and perform the telnet email test mentioned earlier in the chapter, only this time, connect to your incoming mail server (whatever mail server has the highest priority MX record), and address the email to you or the user that is complaining about an email not going through. If your mail server accepts your telnet test and the email shows up in the recipient’s mailbox, you can be relatively sure general incoming mail is being accepted for that user.

# ## Telnet Test Can’t Connect

There are a few ways the telnet test can fail, however. For one, you might discover you can’t connect to your mail server from the outside at all; in this case, it’s time to log in to the incoming mail server and make sure the mail server software is running. For instance, on a system running postfix, you might type

```
$ sudo /etc/init.d/postfix status
● postfix is running
```

If you are running sendmail or exim, you can replace postfix with the name of your server’s init script. Alternatively, you can also simply check