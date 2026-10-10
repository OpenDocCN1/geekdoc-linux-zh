+   - The first line causes Fetchmail to run in daemon mode and check for new mail every 600 seconds (10 minutes). When Fetchmail is started, it will check for new mail and move itself into the background as a daemon. After that, it will check for new mail every 600 seconds. If this line is not present, when you invoke Fetchmail, it will check for new mail and then terminate immediately and not check again.
+   - The second line is the fallback address. Basically, any mail that Fetchmail receives that is not addressed to a local user will be sent to this account on the local system. You should probably set this to the same user you will be running Fetchmail as.
+   - Finally, the third option sets a log file in which Fetchmail will log its activity. Alternatively, you can use the line set syslog instead, which will cause Fetchmail to use syslogd for logging. syslogd is the system-logging daemon that handles the logging of other system events.

The next section of the `.fetchmailrc` file is the server section, which contains information on each mail server that should be checked for mail. Here is a sample server section that is configured to check one e-mail server:

```
poll mail.sample.net.org
proto pop3
no dns
```

Several other server options are available. See the Fetchmail man page for full details. Here are the options shown in this example:

+   - The first line causes the server `mail.sample.net.org` to be checked for new mail at the interval configured by the `set daemon` option in the global section, as well as each time Fetchmail is invoked manually. The alternative would be `skip mail.sample.net.org`. In this case, this server would be skipped and not checked for new mail at the regular intervals or when Fetchmail is invoked manually. If the `skip` option is used, the server will only be checked for new mail when it is specified on the command line when invoking Fetchmail.
+   - The second line tells Fetchmail the protocol to use with this server. In this case, it is POP3. Other legal options are POP3, IMAP, APop, APOP, and KPOP.
+   - The third option tells Fetchmail not to perform DNS lookups on multidrop. If you are running over a dial-up Internet connection, you will probably want to include this line.

The third and final section of the `.fetchmailrc` file is the user section, which contains information about the account itself. Here is a sample user section of `.fetchmailrc`:

```
user foobar
pass secretword
```