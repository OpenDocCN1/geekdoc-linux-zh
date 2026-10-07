This command tells Sendmail to process the queue once when it is started, and again only when you manually direct it to do so. To manually tell Sendmail to process the queue, you can use a command like the following:

```
# sendmail -q
```

> There is a configuration file for pppd called ppp.link, which is located in /etc/ppp. Any commands in this file will be automatically run each time the PPP daemon is started. You can add the line sendmail -q to this file to have mail queue automatically processed each time you dial your Internet connection.

# Building the sendmail.cf File

Books are available to explore the depths of Sendmail configuration, but the Sendmail Installation and Operation Guide is the canonical reference. Configuration guidance can also be found through a Google search; many people use Sendmail in many different configurations. Fortunately, Red Hat has provided a default Sendmail configuration that will work "out-of-the-box" for a home user as long as your networking is correctly configured and you don't require an ISP-like specific configuration.

After you have made all changes to sendmail.cf, you need to rebuild the sendmail.cf file. First, back up your old file:

```
# mv /etc/mail/sendmail.cf /etc/mail/sendmail.cf.old
```

You must run sendmail.mc through the m4 processor to generate a usable configuration file. A command, as the following, is used to do this:

```
# m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

This command loads the cf.m4 macro file from /usr/share/sendmail-cf/m4/cf.m4 and then uses it to process the sendmail.mc file. The output, normally sends to STDOUT, and you need redirected to the file sendmail.cf, and your new configuration file is ready. You will need to restart Sendmail before the changes take effect.

# Mail Relaying

By default, Sendmail will not relay mail that didn't originate from the local domain. This means that if a Sendmail installation running at lion.org receives mail intended for cheetah.org, and that didn't originate from lion.org, the mail will be rejected and not relayed. If you want to allow selected domains to relay through, add an entry for the domain to the file /etc/relay-domains.mc. If the file doesn't exist, simply create it in your favorite text editor and add a line containing the name of the domain that you