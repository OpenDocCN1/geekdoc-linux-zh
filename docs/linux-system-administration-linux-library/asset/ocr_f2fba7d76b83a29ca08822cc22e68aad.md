# Configuring POP and IMAP 595

> **TIP** Rather than directly editing the .fetchmailrc file, you may want to try fetchmailconf. This utility, which is installed separately from fetchmail in Red Hat 7.0, is a GUI configuration tool for fetchmail. Using this tool can ensure you generate a usable .fetchmailrc file.

> **WARNING** Because the .fetchmailrc file contains passwords, it's critically important that this file be protected from unauthorized access. In fact, fetchmail refuses to run if .fetchmailrc can be read by anybody but the owner.

# Using fetchmail

Once you've configured fetchmail, you should test it. You can do so with the following command:

```
$ fetchmail -d0 -k
```

The -d0 option ensures that fetchmail does not enter daemon mode; this invocation will be a one-time call, even if .fetchmailrc specifies daemon mode. Likewise, -k tells fetchmail to leave retrieved messages on the mail server. This ensures that you won't lose your mail if there's a problem that causes the mail to be lost between retrieval and injection into your local mail queue.

Once you've tested your fetchmail configuration and worked out any kinks, you can set it up for regular use. There are several possible ways to do this:

+   - You can use fetchmail's daemon mode to have it stay active and check for mail at regular intervals. If you want fetchmail to start automatically when the computer boots, you'll need to add an appropriate entry to a start-up file, such as /etc/rc.d/rc.local. Unfortunately, some people find fetchmail occasionally crashes, so this mode may not be the best choice if you need the reliability.
- You can run fetchmail from a cron job. For instance, to have fetchmail retrieve mail every hour, you can create a simple script (see Chapter 14) to do this and place it in /etc/cron.hourly. If you use this approach, be sure to specify daemon mode in your .fetchmailrc file.
- You can run fetchmail as part of a network start-up script. This approach is particularly useful for those who use PPP dial-up accounts, because you can configure the system to start fetchmail when the Internet connection initializes and to shut down when the connection ends.

![](bbox=[0.935, 0.635, 0.965, 0.735])

PART 5